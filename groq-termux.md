
---

# 1. Setup Once

## Install the required packages

```bash
pkg update && pkg upgrade -y
pkg install jq curl fzf termux-api termux-tools python -y
```

Optional Python SDK:

```bash
pip install groq
```

If `pip` complains about the environment, use:

```bash
python -m pip install groq
```

---

## Configure your Groq API key

### Simple method

```bash
echo 'export GROQ_API_KEY="gsk_..."' >> ~/.bashrc
source ~/.bashrc
```

Replace `gsk_...` with your actual Groq API key.

Check that it exists without printing the key:

```bash
if [ -n "$GROQ_API_KEY" ]; then
    echo "GROQ_API_KEY is set"
else
    echo "GROQ_API_KEY is NOT set"
fi
```

### More secure alternative

Instead of putting the key directly into `.bashrc`, store it in a separate file:

```bash
cat > ~/.groq_env <<'EOF'
export GROQ_API_KEY="gsk_..."
EOF

chmod 600 ~/.groq_env
source ~/.groq_env
```

Then add this to `~/.bashrc`:

```bash
[ -f ~/.groq_env ] && source ~/.groq_env
```

This keeps the API key separate from the rest of your shell configuration.

> **Do not commit `.bashrc`, `.groq_env`, or files containing your API key to GitHub.**

---

# 2. Optional Groq Alias

A reusable API endpoint alias:

```bash
echo 'alias groq20="curl -sS -X POST https://api.groq.com/openai/v1/chat/completions -H \"Authorization: Bearer \$GROQ_API_KEY\" -H \"Content-Type: application/json\""' >> ~/.bashrc
```

Reload:

```bash
source ~/.bashrc
```

You can now build requests around:

```bash
groq20
```

---

# 3. Fix Termux Repository / Mirror Problems

If Termux reports a repository or mirror problem:

```bash
termux-change-repo
```

Select an appropriate main repository mirror.

If you use the Termux extra repositories, keep the repositories you actually need enabled.

Then:

```bash
pkg update
```

---

# 4. Shell History Quality of Life

Increase history size and remove duplicate commands:

```bash
cat >> ~/.bashrc <<'EOF'

# Large persistent shell history
export HISTSIZE=100000
export HISTFILESIZE=100000
shopt -s histappend
export HISTCONTROL=ignoredups:erasedups

# Up/down arrows search history using the current command prefix
bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
EOF
```

Reload:

```bash
source ~/.bashrc
```

For example, type:

```text
curl
```

and press ↑ to cycle through previous commands beginning with `curl`.

---

# 5. Verify Everything

Check the important tools:

```bash
command -v curl
command -v jq
command -v fzf
command -v termux-clipboard-get
command -v termux-clipboard-set
python --version
```

Check the API key:

```bash
if [ -n "$GROQ_API_KEY" ]; then
    echo "Groq API key detected"
else
    echo "Groq API key missing"
fi
```

---

# 6. Core Groq Requests

Groq exposes an OpenAI-compatible chat completions API.

Endpoint:

```text
https://api.groq.com/openai/v1/chat/completions
```

---

## Basic non-reasoning request

Example using `llama-3.3-70b-versatile`:

```bash
curl -sS https://api.groq.com/openai/v1/chat/completions \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama-3.3-70b-versatile",
    "messages": [
      {
        "role": "user",
        "content": "Explain quicksort."
      }
    ],
    "temperature": 0.7
  }' |
jq -r '.choices[0].message.content'
```

---

## Reasoning model — GPT-OSS 20B

```bash
curl -sS https://api.groq.com/openai/v1/chat/completions \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-oss-20b",
    "messages": [
      {
        "role": "user",
        "content": "Solve: 3x + 5 = 20"
      }
    ],
    "reasoning_format": "parsed",
    "reasoning_effort": "low",
    "temperature": 0.7,
    "max_tokens": 2048
  }' |
jq .
```

Typical reasoning effort values for GPT-OSS:

```text
low
medium
high
```

General idea:

| Setting  | Purpose                  |
| -------- | ------------------------ |
| `low`    | Faster / less reasoning  |
| `medium` | More reasoning           |
| `high`   | Maximum reasoning effort |

For models with different reasoning controls, check the model's current API documentation before assuming the same parameters apply.

---

# 7. Streaming Responses

Streaming allows the response to appear progressively instead of waiting for the entire response.

```bash
curl -sS https://api.groq.com/openai/v1/chat/completions \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-oss-20b",
    "messages": [
      {
        "role": "user",
        "content": "Write a short science-fiction story."
      }
    ],
    "reasoning_format": "hidden",
    "stream": true
  }' |
while IFS= read -r line; do
    case "$line" in
        data:\ *)
            json="${line#data: }"

            if [ "$json" = "[DONE]" ]; then
                break
            fi

            printf '%s' "$json" |
                jq -r 'select(.choices[0].delta.content) | .choices[0].delta.content' 2>/dev/null
            ;;
    esac
done

printf '\n'
```

---

# 8. `jq` Bible for Groq

The API normally returns JSON.

`jq` makes the response much easier to work with.

---

## Pretty-print the entire response

```bash
jq .
```

---

## Print only the answer

```bash
jq -r '.choices[0].message.content'
```

---

## Print reasoning

For responses using parsed reasoning:

```bash
jq -r '.choices[0].message.reasoning'
```

---

## Print reasoning and answer separately

```bash
jq -r '
  "REASONING:\n\(.choices[0].message.reasoning // "")\n\nANSWER:\n\(.choices[0].message.content // "")"
'
```

---

## Print model and token statistics

```bash
jq '{
  model: .model,
  tokens_prompt: .usage.prompt_tokens,
  tokens_completion: .usage.completion_tokens,
  total_tokens: .usage.total_tokens,
  time: .usage.total_time
}'
```

---

## Show the API error if one exists

```bash
jq '.error // .'
```

A useful general-purpose pattern:

```bash
jq -r '
  if .error then
    "ERROR: \(.error.message // .error)"
  else
    .choices[0].message.content // ""
  end
'
```

---

# 9. Save Raw Responses

Instead of immediately throwing away the complete JSON response:

```bash
curl -sS https://api.groq.com/openai/v1/chat/completions \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama-3.3-70b-versatile",
    "messages": [
      {
        "role": "user",
        "content": "Explain black holes."
      }
    ]
  }' |
tee last_raw.json |
jq -r '.choices[0].message.content'
```

You now have:

```text
last_raw.json
```

containing the complete API response.

---

# 10. The `ask` Function

This is the main interactive workflow.

It:

1. Accepts a prompt
2. Sends it to Groq
3. Saves the raw response
4. Extracts the answer
5. Saves the clean answer
6. Copies the answer to the Android clipboard

Add this to `~/.bashrc`:

```bash
ask() {
    if [ -z "$GROQ_API_KEY" ]; then
        echo "ERROR: GROQ_API_KEY is not set."
        return 1
    fi

    if [ "$#" -eq 0 ]; then
        echo 'Usage: ask "your prompt here"'
        return 1
    fi

    local prompt="$*"
    local raw_file="$HOME/last_raw.json"
    local answer_file="$HOME/last_answer.txt"
    local request_file
    request_file="$(mktemp)"

    jq -n \
        --arg model "openai/gpt-oss-20b" \
        --arg content "$prompt" \
        '{
            model: $model,
            messages: [
                {
                    role: "user",
                    content: $content
                }
            ],
            reasoning_format: "parsed",
            reasoning_effort: "low"
        }' > "$request_file"

    curl -sS \
        -X POST \
        "https://api.groq.com/openai/v1/chat/completions" \
        -H "Authorization: Bearer $GROQ_API_KEY" \
        -H "Content-Type: application/json" \
        --data-binary "@$request_file" |
        tee "$raw_file" |
        jq -e '.error' >/dev/null 2>&1

    local error_status=$?

    if [ "$error_status" -eq 0 ]; then
        echo "Groq API error:"
        jq '.error' "$raw_file"
        rm -f "$request_file"
        return 1
    fi

    jq -r '.choices[0].message.content // empty' \
        "$raw_file" |
        tee "$answer_file"

    local answer_status=${PIPESTATUS[0]}

    if [ "$answer_status" -ne 0 ]; then
        echo "ERROR: Could not extract the answer."
        rm -f "$request_file"
        return 1
    fi

    if command -v termux-clipboard-set >/dev/null 2>&1; then
        cat "$answer_file" | termux-clipboard-set
        echo
        echo "[Answer copied to clipboard]"
    fi

    rm -f "$request_file"
}
```

Reload:

```bash
source ~/.bashrc
```

Usage:

```bash
ask "Explain black holes like I'm five."
```

Or:

```bash
ask "Write a Bash script that finds files larger than 100 MB."
```

---

# 11. Ask From Android Clipboard

This lets you copy something anywhere on Android and send it directly to Groq.

Add:

```bash
askclip() {
    if ! command -v termux-clipboard-get >/dev/null 2>&1; then
        echo "ERROR: termux-api is not installed."
        return 1
    fi

    local prompt
    prompt="$(termux-clipboard-get)"

    if [ -z "$prompt" ]; then
        echo "Clipboard is empty."
        return 1
    fi

    ask "$prompt"
}
```

Reload:

```bash
source ~/.bashrc
```

Usage:

```bash
askclip
```

Workflow:

```text
Copy text on Android
        ↓
     askclip
        ↓
      Groq
        ↓
Answer copied back to clipboard
```

---

# 12. Save and Reuse Prompts

Create a persistent prompt file:

```bash
echo 'Explain this like a senior Linux administrator:' > ~/.last_prompt
```

Run it:

```bash
ask "$(cat ~/.last_prompt)"
```

A convenient helper:

```bash
lastprompt() {
    if [ ! -f "$HOME/.last_prompt" ]; then
        echo "No saved prompt."
        return 1
    fi

    cat "$HOME/.last_prompt"
}
```

Then:

```bash
lastprompt
```

---

# 13. Interactive Prompt Saver

Add:

```bash
saveprompt() {
    if [ "$#" -eq 0 ]; then
        echo 'Usage: saveprompt "your prompt"'
        return 1
    fi

    printf '%s\n' "$*" > "$HOME/.last_prompt"

    echo "Saved:"
    cat "$HOME/.last_prompt"
}
```

Usage:

```bash
saveprompt "Analyse this shell script for security problems."
```

Then:

```bash
ask "$(cat ~/.last_prompt)"
```

---

# 14. Multi-Turn Conversations

Create a conversation file:

```bash
cat > "$HOME/chat.json" <<'JSON'
[
  {
    "role": "system",
    "content": "You are an expert Linux and Android systems administrator."
  }
]
JSON
```

Add the following function to `~/.bashrc`:

```bash
chat() {
    if [ -z "$GROQ_API_KEY" ]; then
        echo "ERROR: GROQ_API_KEY is not set."
        return 1
    fi

    if [ "$#" -eq 0 ]; then
        echo 'Usage: chat "your message"'
        return 1
    fi

    local message="$*"
    local request_file
    local response_file
    local new_history

    request_file="$(mktemp)"
    response_file="$(mktemp)"
    new_history="$(mktemp)"

    if [ ! -f "$HOME/chat.json" ]; then
        printf '%s\n' '[]' > "$HOME/chat.json"
    fi

    jq \
        --arg content "$message" \
        '. + [{"role":"user","content":$content}]' \
        "$HOME/chat.json" > "$new_history" || {
            echo "ERROR: Could not update conversation."
            rm -f "$request_file" "$response_file" "$new_history"
            return 1
        }

    mv "$new_history" "$HOME/chat.json"

    jq -n \
        --arg model "openai/gpt-oss-20b" \
        --slurpfile messages "$HOME/chat.json" \
        '{
            model: $model,
            messages: $messages[0],
            reasoning_format: "hidden",
            reasoning_effort: "low"
        }' > "$request_file"

    curl -sS \
        -X POST \
        "https://api.groq.com/openai/v1/chat/completions" \
        -H "Authorization: Bearer $GROQ_API_KEY" \
        -H "Content-Type: application/json" \
        --data-binary "@$request_file" |
        tee "$response_file" >/dev/null

    if jq -e '.error' "$response_file" >/dev/null 2>&1; then
        echo "Groq API error:"
        jq '.error' "$response_file"
        rm -f "$request_file" "$response_file"
        return 1
    fi

    local answer
    answer="$(jq -r '.choices[0].message.content // empty' "$response_file")"

    if [ -z "$answer" ]; then
        echo "ERROR: Empty response."
        rm -f "$request_file" "$response_file"
        return 1
    fi

    printf '%s\n' "$answer"

    jq \
        --arg content "$answer" \
        '. + [{"role":"assistant","content":$content}]' \
        "$HOME/chat.json" > "$new_history" || {
            echo "ERROR: Could not save assistant response."
            rm -f "$request_file" "$response_file" "$new_history"
            return 1
        }

    mv "$new_history" "$HOME/chat.json"

    rm -f "$request_file" "$response_file"
}
```

Reload:

```bash
source ~/.bashrc
```

Usage:

```bash
chat "How do I find the largest files in Linux?"
```

Then:

```bash
chat "Modify that command so it ignores /proc."
```

The previous conversation remains in:

```text
~/chat.json
```

---

# 15. Reset a Conversation

Start again:

```bash
printf '%s\n' '[]' > ~/chat.json
```

Or preserve the old conversation first:

```bash
cp ~/chat.json "chat-$(date +%Y%m%d-%H%M%S).json"
printf '%s\n' '[]' > ~/chat.json
```

---

# 16. FZF History Search

Install:

```bash
pkg install fzf -y
```

Add a proper fuzzy history function:

```bash
fzf-history() {
    local selected
    selected="$(
        fc -rl 1 |
        awk '!seen[$0]++' |
        fzf --tac --no-sort
    )"

    if [ -n "$selected" ]; then
        READLINE_LINE="$selected"
        READLINE_POINT=${#READLINE_LINE}
    fi
}
```

Bind it to `Ctrl+R`:

```bash
bind -x '"\C-r": fzf-history'
```

Reload:

```bash
source ~/.bashrc
```

Now:

```text
Ctrl+R
```

opens a fuzzy search through your shell history.

---

# 17. Logging Everything

To record a complete Termux session:

```bash
script -a "$HOME/termux_session.log"
```

Everything typed and printed during the session is recorded.

Stop logging with:

```bash
exit
```

View the log:

```bash
less ~/termux_session.log
```

Search it:

```bash
grep -n "groq" ~/termux_session.log
```

---

# 18. Retry Wrapper

A basic retry wrapper for commands that occasionally fail:

```bash
retry() {
    local attempts="${1:-3}"
    shift

    local delay=2
    local attempt

    for ((attempt=1; attempt<=attempts; attempt++)); do
        "$@" && return 0

        if [ "$attempt" -lt "$attempts" ]; then
            echo "Attempt $attempt failed. Retrying in ${delay}s..."
            sleep "$delay"
            delay=$((delay * 2))
        fi
    done

    echo "Command failed after $attempts attempts."
    return 1
}
```

Example:

```bash
retry 3 curl -fsS https://example.com
```

---

# 19. Groq-Specific Retry Helper

For API calls, it is usually better to retry the entire request rather than pipe partial output through `jq`.

```bash
groq_request() {
    if [ -z "$GROQ_API_KEY" ]; then
        echo "ERROR: GROQ_API_KEY is not set."
        return 1
    fi

    local request_file="$1"
    local output_file="$2"

    if [ ! -f "$request_file" ]; then
        echo "ERROR: Request file does not exist: $request_file"
        return 1
    fi

    local attempt
    local http_code

    for attempt in 1 2 3; do
        http_code="$(
            curl -sS \
                -o "$output_file" \
                -w '%{http_code}' \
                -X POST \
                "https://api.groq.com/openai/v1/chat/completions" \
                -H "Authorization: Bearer $GROQ_API_KEY" \
                -H "Content-Type: application/json" \
                --data-binary "@$request_file"
        )"

        if [[ "$http_code" =~ ^2[0-9][0-9]$ ]]; then
            return 0
        fi

        echo "Groq HTTP $http_code on attempt $attempt."

        if [ "$attempt" -lt 3 ]; then
            sleep $((attempt * 2))
        fi
    done

    echo "Groq request failed."
    jq '.error // .' "$output_file" 2>/dev/null || cat "$output_file"

    return 1
}
```

---

# 20. List Available Models

List the models currently exposed by your Groq API account:

```bash
curl -sS \
  "https://api.groq.com/openai/v1/models" \
  -H "Authorization: Bearer $GROQ_API_KEY" |
jq -r '.data[].id' |
sort
```

Pipe into FZF:

```bash
curl -sS \
  "https://api.groq.com/openai/v1/models" \
  -H "Authorization: Bearer $GROQ_API_KEY" |
jq -r '.data[].id' |
sort |
fzf
```

---

# 21. Model Selection

Model availability changes over time, so don't hard-code assumptions about which model is currently available.

Useful examples historically used with Groq include:

```text
llama-3.1-8b-instant
llama-3.3-70b-versatile
openai/gpt-oss-20b
openai/gpt-oss-120b
qwen/qwen3-32b
```

Always verify your current account's model list:

```bash
curl -sS \
  "https://api.groq.com/openai/v1/models" \
  -H "Authorization: Bearer $GROQ_API_KEY" |
jq -r '.data[].id' |
sort
```

> **Important:** Model names, availability, capabilities, and parameters can change. Treat the live `/models` endpoint and current Groq documentation as authoritative rather than relying on an old cheatsheet.

---

# 22. Quick Model Picker

Create:

```bash
groqmodel() {
    curl -sS \
        "https://api.groq.com/openai/v1/models" \
        -H "Authorization: Bearer $GROQ_API_KEY" |
    jq -r '.data[].id' |
    sort |
    fzf
}
```

Usage:

```bash
groqmodel
```

Select a model with FZF.

---

# 23. Termux Notification

If you want Android to notify you when a long request finishes:

```bash
termux-notification \
    --title "Groq" \
    --content "Groq request finished"
```

With vibration:

```bash
termux-notification \
    --title "Groq" \
    --content "Groq request finished" \
    --vibrate 200
```

For example:

```bash
ask "Analyse this 500-line Bash script."
termux-notification \
    --title "Groq" \
    --content "Analysis complete" \
    --vibrate 200
```

---

# 24. Clipboard Utilities

Copy a file to the Android clipboard:

```bash
cat last_answer.txt | termux-clipboard-set
```

Read the Android clipboard:

```bash
termux-clipboard-get
```

Copy the current answer:

```bash
termux-clipboard-set < ~/last_answer.txt
```

---

# 25. Quick Groq Health Check

A simple check:

```bash
groqcheck() {
    if [ -z "$GROQ_API_KEY" ]; then
        echo "ERROR: GROQ_API_KEY is not set."
        return 1
    fi

    local response

    response="$(
        curl -sS \
            "https://api.groq.com/openai/v1/models" \
            -H "Authorization: Bearer $GROQ_API_KEY"
    )"

    if echo "$response" | jq -e '.error' >/dev/null 2>&1; then
        echo "Groq authentication/API error:"
        echo "$response" | jq '.error'
        return 1
    fi

    echo "$response" |
        jq -r '
            if (.data | length) > 0
            then "Key OK — API reachable"
            else "API reachable but no models returned"
            end
        '
}
```

Run:

```bash
groqcheck
```

---

# 26. Check API Key Without Revealing It

Never do this:

```bash
echo "$GROQ_API_KEY"
```

Instead:

```bash
if [ -n "$GROQ_API_KEY" ]; then
    echo "API key is configured."
else
    echo "API key is missing."
fi
```

You can also display only a small prefix:

```bash
if [ -n "$GROQ_API_KEY" ]; then
    printf 'Configured: %.6s...\n' "$GROQ_API_KEY"
else
    echo "Not configured."
fi
```

Avoid logging commands containing the full key.

---

# 27. Useful Files

A practical layout:

```text
$HOME/
├── .bashrc
├── .groq_env
├── .last_prompt
├── chat.json
├── last_raw.json
├── last_answer.txt
├── termux_session.log
└── cheatsheet.md
```

Recommended permissions:

```bash
chmod 600 ~/.groq_env
chmod 600 ~/chat.json
chmod 600 ~/last_raw.json
```

---

# 28. One-Command `ask` Workflow

The intended workflow is:

```text
Android clipboard
       │
       ▼
   askclip
       │
       ▼
    Groq API
       │
       ▼
  last_raw.json
       │
       ▼
 last_answer.txt
       │
       ▼
 Android clipboard
```

For normal prompts:

```bash
ask "Explain how DNS resolution works."
```

For clipboard content:

```bash
askclip
```

For a persistent conversation:

```bash
chat "Start a new Linux troubleshooting session."
```

---

# 29. Useful Aliases

Add these to `~/.bashrc`:

```bash
alias ll='ls -lah'
alias la='ls -A'
alias c='clear'

alias groqmodels='curl -sS https://api.groq.com/openai/v1/models -H "Authorization: Bearer $GROQ_API_KEY" | jq -r ".data[].id" | sort'

alias groqlast='jq -r ".choices[0].message.content // .error.message // ." ~/last_raw.json'

alias groqstats='jq ".usage // {}" ~/last_raw.json'

alias groqjson='jq . ~/last_raw.json'

alias groqanswer='cat ~/last_answer.txt'

alias chatreset='printf "%s\n" "[]" > ~/chat.json'
```

Reload:

```bash
source ~/.bashrc
```

---

# 30. Inspect the Last Response

Pretty-print:

```bash
groqjson
```

Only answer:

```bash
groqlast
```

Token usage:

```bash
groqstats
```

Clean answer:

```bash
groqanswer
```

---

# 31. Useful JSON Request Template

When experimenting with parameters, start with:

```json
{
  "model": "MODEL_ID",
  "messages": [
    {
      "role": "user",
      "content": "YOUR PROMPT"
    }
  ]
}
```

Then add only the parameters supported by the selected model.

For example:

```json
{
  "model": "openai/gpt-oss-20b",
  "messages": [
    {
      "role": "user",
      "content": "Solve this problem."
    }
  ],
  "reasoning_format": "parsed",
  "reasoning_effort": "medium"
}
```

---

# 32. Roles

Typical chat messages use:

```json
{
  "role": "system",
  "content": "You are an expert Linux administrator."
}
```

```json
{
  "role": "user",
  "content": "How do I inspect open network connections?"
}
```

```json
{
  "role": "assistant",
  "content": "Use ss..."
}
```

A conversation therefore looks like:

```json
[
  {
    "role": "system",
    "content": "You are an expert Linux administrator."
  },
  {
    "role": "user",
    "content": "How do I inspect open network connections?"
  },
  {
    "role": "assistant",
    "content": "Use ss..."
  },
  {
    "role": "user",
    "content": "How do I filter that to TCP?"
  }
]
```

---

# 33. Important `curl` Flags

Useful flags to remember:

```bash
-s
```

Silent mode.

```bash
-S
```

Show errors even when silent.

Together:

```bash
-sS
```

Usually preferable for scripts.

```bash
-f
```

Fail on HTTP errors.

```bash
-o file
```

Write output to a file.

```bash
-w '%{http_code}'
```

Print the HTTP status code.

```bash
-X POST
```

Use POST.

```bash
-H "Content-Type: application/json"
```

Set a request header.

```bash
--data-binary @file.json
```

Send JSON from a file.

---

# 34. HTTP Status Codes

Useful when debugging:

|  Code | Meaning                        |
| ----: | ------------------------------ |
| `200` | Request succeeded              |
| `400` | Bad request                    |
| `401` | Authentication problem         |
| `403` | Forbidden                      |
| `404` | Endpoint/resource not found    |
| `429` | Rate limit / too many requests |
| `500` | Server error                   |
| `502` | Bad gateway                    |
| `503` | Service unavailable            |

Check the HTTP code directly:

```bash
curl -sS \
  -o response.json \
  -w 'HTTP %{http_code}\n' \
  "https://api.groq.com/openai/v1/models" \
  -H "Authorization: Bearer $GROQ_API_KEY"
```

Then inspect:

```bash
jq . response.json
```

---

# 35. Debugging a Failed Request

If something isn't working, save the complete response:

```bash
curl -sS \
  -o response.json \
  -w 'HTTP %{http_code}\n' \
  -X POST \
  "https://api.groq.com/openai/v1/chat/completions" \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-oss-20b",
    "messages": [
      {
        "role": "user",
        "content": "Hello"
      }
    ]
  }'
```

Inspect:

```bash
jq . response.json
```

If it contains:

```json
{
  "error": {
    "message": "..."
  }
}
```

the error message is usually the first thing to investigate.

---

# 36. Keep Your API Key Out of Git

If this directory is a Git repository:

```bash
printf '%s\n' '.groq_env' >> .gitignore
printf '%s\n' 'last_raw.json' >> .gitignore
printf '%s\n' 'chat.json' >> .gitignore
printf '%s\n' '*.log' >> .gitignore
```

Check what Git sees:

```bash
git status
```

Search the current directory for accidental API-key exposure:

```bash
grep -R "gsk_" . --exclude-dir=.git 2>/dev/null
```

If a key has accidentally been committed or exposed, **revoke/rotate it immediately** rather than merely deleting the file.

---

# 37. Recommended `.bashrc` Structure

Keep API configuration separate from functions.

For example:

```bash
# ==========================================
# General shell settings
# ==========================================

export HISTSIZE=100000
export HISTFILESIZE=100000
shopt -s histappend
export HISTCONTROL=ignoredups:erasedups

bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'


# ==========================================
# Groq credentials
# ==========================================

[ -f "$HOME/.groq_env" ] && source "$HOME/.groq_env"


# ==========================================
# Groq aliases
# ==========================================

alias groqmodels='curl -sS https://api.groq.com/openai/v1/models -H "Authorization: Bearer $GROQ_API_KEY" | jq -r ".data[].id" | sort'

alias groqjson='jq . ~/last_raw.json'

alias groqlast='jq -r ".choices[0].message.content // .error.message // ." ~/last_raw.json'

alias groqstats='jq ".usage // {}" ~/last_raw.json'

alias groqanswer='cat ~/last_answer.txt'


# ==========================================
# Groq functions
# ==========================================

# Add ask()
# Add askclip()
# Add chat()
# Add groqcheck()
# Add groqmodel()
# Add retry()
# Add fzf-history()
```

---

# 38. Final Quick Reference

## Authentication

```bash
source ~/.groq_env
```

## Check API

```bash
groqcheck
```

## List models

```bash
groqmodels
```

## Ask a question

```bash
ask "Explain TCP/IP."
```

## Ask using clipboard

```bash
askclip
```

## Start/continue conversation

```bash
chat "Explain how Android permissions work."
```

## Reset conversation

```bash
chatreset
```

## View last answer

```bash
groqanswer
```

## View complete response

```bash
groqjson
```

## View token statistics

```bash
groqstats
```

## Copy last answer

```bash
termux-clipboard-set < ~/last_answer.txt
```

## Fuzzy shell history

```text
Ctrl + R
```

## Log a complete Termux session

```bash
script -a ~/termux_session.log
```

## Stop logging

```bash
exit
```

---

# 39. Minimal First-Time Setup

If you want the shortest possible setup:

```bash
pkg update && pkg upgrade -y
pkg install jq curl fzf termux-api termux-tools python -y

cat > ~/.groq_env <<'EOF'
export GROQ_API_KEY="gsk_..."
EOF

chmod 600 ~/.groq_env

cat >> ~/.bashrc <<'EOF'

[ -f "$HOME/.groq_env" ] && source "$HOME/.groq_env"

export HISTSIZE=100000
export HISTFILESIZE=100000
shopt -s histappend
export HISTCONTROL=ignoredups:erasedups

bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
EOF

source ~/.bashrc
```

Verify:

```bash
groqcheck
```

Then make your first request:

```bash
curl -sS \
  https://api.groq.com/openai/v1/chat/completions \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "openai/gpt-oss-20b",
    "messages": [
      {
        "role": "user",
        "content": "Hello from Termux."
      }
    ]
  }' |
jq -r '.choices[0].message.content // .error.message // .'
```

---



The most useful commands to remember are:

```bash
ask "your question"
```

```bash
askclip
```

```bash
chat "continue the conversation"
```

```bash
groqcheck
```

```bash
groqmodels
```

```bash
groqjson
```

```bash
groqanswer
```

```bash
groqstats
```

```text
Ctrl+R
```

That gives you a compact **Android-native Groq CLI workstation** without needing Node, npm, a server, or a desktop environment.
