`

kiosk_touch_defense_audit/
├── 01_SystemUI_and_Kiosk_Lockdown_Boundaries/
│⠀⠀⠀├── 1.1_Top_Edge_StatusBar_Pull_Isolation/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Execute single- and two-finger downward swipes starting from the top bezel edge across all customer screens (idle ad loop, item grid, cart, payment modal).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test rapid consecutive "double-pull" swipes used to expand Quick Settings, slow micro-drags across the upper 10px bezel margin, and swipes immediately following a modal popup transition when immersive flags momentarily reset.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Status bar and Quick Settings shade remain completely suppressed (LockTask / STATUS_BAR_DISABLE_EXPAND enforced); transient translucent bars, if briefly visible on legacy AOSP builds, accept zero touch input and auto-retract within <500ms.
│⠀⠀⠀│
│⠀⠀⠀├── 1.2_Bottom_Edge_Navigation_Gesture_Suppression/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Perform upward swipes and hold gestures from the bottom screen edge to test for AOSP 3-button navbar reveal or Android 10+ gesture navigation Home/Overview triggers.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test angled upward flicks from bottom-left and bottom-right corners (Google Assistant corner triggers on Android 9–11) and bottom-edge swipes while a system-level dialog (e.g., network/payment timeout) has focus.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Navigation bar remains hidden and non-interactive; upward edge gestures do not minimize the vending APK or invoke Assistant/Recents overlays.
│⠀⠀⠀│
│⠀⠀⠀├── 1.3_Lateral_Edge_Back_Swipe_Containment/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Execute inward horizontal swipes from both the left and right vertical bezels across nested UI views (Sort filters, Shopping Cart, Help, and checkout modals).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test lateral edge swipes while an embedded WebView or media carousel is active to verify whether OS-level onBackPressed() exits the kiosk activity to the underlying launcher.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Lateral edge gestures are either consumed by internal app navigation or ignored; the kiosk activity never backgrounds to the AOSP launcher.
│⠀⠀⠀│
│⠀⠀⠀├── 1.4_Multi_Finger_SplitScreen_and_Recents_Triggers/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Apply 3-finger vertical swipes, 3-finger pinch gestures, and 4-finger inward sweeps commonly mapped by Rockchip/Allwinner vendor ROMs to screenshot, split-screen, or task-switcher actions.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test vendor-specific ROM gesture shortcuts while holding a single static touch point in the screen center (multi-pointer chord triggers).
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Vendor ROM multi-finger gestures are disabled at the framework/policy level; no screenshot toast, split-screen divider, or task switcher appears.
│⠀⠀⠀│
│⠀⠀⠀├── 1.5_Hardware_Key_and_Touch_Combo_Interception/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Inspect the bezel perimeter for recessed pinhole buttons or capacitive soft-keys, and test touch-plus-bezel edge pressure combinations during boot or app relaunch.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test capacitive touch responsiveness during the brief window between Android boot animation completion and kiosk launcher initialization.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: No external physical buttons are exposed; kiosk application is bound as the sole persistent HOME launcher with LockTask auto-engagement on boot.
│⠀⠀⠀│
│⠀⠀⠀├── 1.6_Screen_Pinning_and_LockTask_Exit_Resilience/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Attempt standard Android unpinning gestures (simultaneous press-and-hold on bottom-left/bottom-right virtual navbar zones) when navigation elements briefly flash during transitions.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test unpinning combinations immediately after triggering an audio alert or orientation/resolution change in media playback.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Kiosk runs under Device Owner LockTask mode rather than user-initiated Screen Pinning, rendering manual unpinning gestures non-functional.
│⠀⠀⠀│
│⠀⠀⠀├── 1.7_System_Toast_and_Dialog_Overlay_ClickThrough/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Observe and tap any Android system toasts or floating overlays (e.g., USB peripheral reconnects, thermal warnings, cellular signal drops, or permission prompts) that render above the kiosk layer.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Rapidly tap the screen coordinates where system dialog action buttons (OK, Settings, Allow, Details) typically appear during MDB peripheral polling.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: System dialogs are suppressed by Device Owner policy; any non-interactive status indicators ignore touch events and pass zero intent escalation paths.
│⠀⠀⠀│
│⠀⠀⠀├── 1.8_Crash_Dialog_App_Info_Intent_Prevention/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: If any UI action triggers an "App keeps stopping" or ANR ("App isn't responding") system modal, test tapping App info or Close app to reach Android Settings.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Repeatedly tap the background behind an ANR dialog to test whether dismissing the dialog exposes the underlying AOSP desktop before the watchdog restarts the kiosk APK.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: System crash/ANR dialogs are suppressed or auto-dismissed silently by a supervisor daemon, immediately relaunching the kiosk foreground activity.
│⠀⠀⠀│
│⠀⠀⠀└── 1.9_Power_Menu_and_Emergency_Call_UI_Suppression/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: Probe screen edges and top-bar status icons for any software power/reboot triggers or lock-screen Emergency dialer buttons during idle sleep/wake cycles.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: Tap the screen repeatedly as the display wakes from screen-saver/dimmed mode to verify no Android lock screen (Keyguard) intercepts the first touch.
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: Keyguard is completely disabled (DISALLOW_KEYGUARD / setKeyguardDisabled); waking the screen lands directly inside the locked kiosk UI with zero dialer or power-menu exposure.
│
├── 02_Hidden_Service_Menus_and_Auth_Gates/
│⠀⠀⠀├── 2.1_Corner_MultiTap_Hotspot_Discovery/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Execute structured multi-tap sequences (5x, 7x, 10x rapid taps within 3 seconds) across all four screen corners, bezel midpoints, and the OEM logo/header region.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test alternating corner tap patterns (e.g., top-left -> top-right -> bottom-right -> bottom-left) and multi-tap triggers specifically on the idle screensaver versus the active product grid.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Either no hidden touch trigger exists (requiring internal physical service button press) or any discovered trigger immediately presents a hardened authentication gate with zero unauthenticated functionality.
│⠀⠀⠀│
│⠀⠀⠀├── 2.2_Status_Badge_LongPress_Trigger_Audit/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Apply sustained press-and-hold gestures (3s, 5s, 10s) on top-bar telemetry indicators (such as the Online connectivity pill, cabinet temperature readout, clock, or machine ID label).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test two-finger simultaneous long-presses on the top status bar and bottom navigation tabs (Home, Sort, Shopping Cart, Help).
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Status indicators are non-interactive display elements or strictly gate maintenance access behind strong technician authentication.
│⠀⠀⠀│
│⠀⠀⠀├── 2.3_Secret_Swipe_Pattern_Sequence_Probing/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Perform directional swipe combinations (e.g., Z-patterns, L-patterns, circular drags, and edge-to-edge cross swipes) on non-scrollable headers and blank background margins.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test gesture sequences immediately after session timeout reset while the UI transitions back to Home.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Unrecognized gesture sequences produce no state change and do not bypass authentication controls.
│⠀⠀⠀│
│⠀⠀⠀├── 2.4_Service_PIN_Keypad_RateLimit_and_Lockout/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Where a technician PIN modal is exposed on the touchscreen, submit consecutive incorrect PIN entries to verify rate-limiting, progressive backoff, and lockout enforcement.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test dismissing and reopening the PIN modal between failed attempts to verify whether the failure counter persists in memory rather than resetting per modal instance.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Failed attempts enforce exponential delay or temporary lockout (e.g., 5 attempts -> 5-minute lock + remote tamper alert) that persists across modal dismissals.
│⠀⠀⠀│
│⠀⠀⠀├── 2.5_Default_and_Factory_PIN_Rejection_Check/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Audit the technician login gate to confirm that factory-default OEM maintenance codes and trivial sequential/repeated numeric patterns have been rotated out prior to deployment.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify whether separate privilege tiers exist (e.g., restocker vs. super-admin) and confirm that both tiers enforce unique, non-default site credentials.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: All factory/OEM default PINs are rejected; authentication requires unique, complex credentials managed per deployment policy.
│⠀⠀⠀│
│⠀⠀⠀├── 2.6_Service_Menu_Session_Idle_AutoExit/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Authenticate into the technician menu using authorized audit credentials, leave the screen untouched, and measure the exact idle timeout before automatic logout.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test idle timeout behavior inside sub-menus (motor test, temperature settings, price configuration) versus the main technician dashboard.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Technician session automatically terminates and returns to the locked customer UI within <=60 seconds of touch inactivity across all sub-menus.
│⠀⠀⠀│
│⠀⠀⠀├── 2.7_Unauthenticated_TestVend_Control_Isolation/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Inspect all customer-accessible screens and pre-auth diagnostic popups for any exposed coil test, motor reset, or manual dispense triggers.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test tapping on 0.00 priced items or unconfigured slots to confirm they do not fall through to a free-vend execution path.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Motor actuation commands (CMD_VEND_SLOT) cannot be dispatched from user space without either a verified MDB payment approval or an authenticated technician session.
│⠀⠀⠀│
│⠀⠀⠀├── 2.8_Diagnostic_Log_and_Telemetry_Screen_Masking/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Review any customer-facing Help, About, or error modals for leaked internal network details (local IP, MAC, IMEI, MQTT broker URL, cloud tenant ID, or Android build fingerprint).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Trigger an offline/network-error state and inspect error codes or troubleshooting text for stack traces or internal file paths.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Customer-facing info screens display only a public asset ID and support contact; all network/API identifiers are masked or restricted to authenticated admin views.
│⠀⠀⠀│
│⠀⠀⠀└── 2.9_Local_Config_Export_and_FilePicker_Blocking/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: Within authorized technician views (e.g., ad media import, log export, price table upload), audit whether interactive controls invoke the native Android DocumentsUI / file picker.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: If a file selector opens, test navigation breadcrumbs, storage root selection, or Open with dialogs that could pivot into Android Settings or third-party apps.
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: Media and configuration sync occurs exclusively via signed cloud OTA pushes; native Android file picker intents are disabled or sandboxed to a restricted directory.
│
├── 03_MultiTouch_Concurrency_and_Input_Fuzzing/
│⠀⠀⠀├── 3.1_Simultaneous_MultiSlot_Selection_Collision/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Tap two or more distinct product tiles simultaneously using multiple fingers on the item grid to observe how the UI handles concurrent touch pointers.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Simultaneously tap a product tile (Slot 14) and the Shopping Cart or Checkout button (ACTION_POINTER_DOWN concurrency).
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Multi-touch pointer events on selection controls are serialized or restricted to primary pointer (pointerId == 0), preventing unintended cart additions or skipped confirmation modals.
│⠀⠀⠀│
│⠀⠀⠀├── 3.2_Rapid_Tap_Debounce_and_DoubleEnqueue/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Execute high-frequency burst taps (10+ taps within 1 second) on a single product card, + quantity incrementer, or Confirm button.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Burst-tap a slot containing only 1 physical unit remaining in stock to test whether UI queueing outpaces inventory decrement checks.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Input debounce (250–400ms cooldown) enforces single-event registration per tap; cart quantity is strictly capped at verified available slot stock.
│⠀⠀⠀│
│⠀⠀⠀├── 3.3_Pinch_Zoom_and_Viewport_Scaling_Lock/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Perform two-finger pinch-in and pinch-out zoom gestures across the product catalog grid, item detail popups, and Help screen.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test double-tap-to-zoom gestures on embedded images or WebView containers.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Viewport scaling is rigidly locked (user-scalable=no / native fixed layout); UI elements neither zoom nor pan off-screen, keeping navigation controls permanently reachable.
│⠀⠀⠀│
│⠀⠀⠀├── 3.4_TwoFinger_Scroll_and_Grid_Desync/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Drag vertically and horizontally with two fingers simultaneously across the slot grid and Shopping Cart list.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Scroll the grid with one finger while tapping slot cards with a second finger to test whether touch coordinate hitboxes desync from visual card positions during momentum scrolling.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Hitboxes remain strictly synchronized with rendered view bounds; scrolling suppresses accidental tap triggers until scroll velocity reaches zero.
│⠀⠀⠀│
│⠀⠀⠀├── 3.5_PressAndHold_Context_Menu_Suppression/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Apply 2-second press-and-hold gestures across product thumbnails, price labels, header banners, and footer icons.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test long-presses specifically on <img> or <video> elements inside hybrid WebView templates where Chrome/WebView defaults to a Save image / Open image popup.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: onLongClick and WebView context menus are globally disabled; holding a finger on any asset produces no browser/OS action sheet.
│⠀⠀⠀│
│⠀⠀⠀├── 3.6_CrossTab_Simultaneous_Tap_Race/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Simultaneously tap two different bottom navigation tabs (Home + Shopping Cart, or Sort + Help) or tap a tab while dismissing an active item modal.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Rapidly alternate taps between Previous and Next pagination controls while simultaneously tapping the Checkout trigger.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Fragment/activity transitions use mutex state locks so concurrent tab presses resolve cleanly to a single deterministic view without overlapping fragments.
│⠀⠀⠀│
│⠀⠀⠀├── 3.7_Ghost_Touch_and_Palm_Rejection_Stability/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Place a broad palm or flat hand across the capacitive glass (simulating moisture/condensation or leaning) and then tap a single product button with a clean fingertip.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Wipe the screen surface with a slightly damp microfiber cloth to simulate high-humidity/condensation ghost touches and verify whether spurious purchases or UI lockups occur.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Touch controller rejects large-area palm contacts without triggering accidental item selections, and normal single-finger responsiveness recovers immediately upon release.
│⠀⠀⠀│
│⠀⠀⠀├── 3.8_Input_Flood_UI_Thread_Watchdog_Recovery/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Subject the touchscreen to sustained 5-finger rapid drumming and continuous circular drags across the entire display for 30 seconds.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Execute the input flood during active serial polling (e.g., right after selecting a slot when the Android app queries VMC slot status).
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: UI thread processes or drops excess motion events gracefully without triggering an ANR, memory leak, or serial command queue corruption.
│⠀⠀⠀│
│⠀⠀⠀└── 3.9_Touch_Coordinate_Boundary_and_OffCanvas_Taps/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: Tap the extreme 1–3px perimeter of modal dialogs, dimmed backdrop overlays, and clipped off-screen list items during scroll transitions.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: Tap the dark modal scrim outside a payment prompt to test whether background grid items underneath still register clicks (click-through bleed).
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: Active modal overlays consume all background touch events; clipped off-canvas elements cannot be activated until scrolled fully into the active viewport.
│
├── 04_Shopping_Cart_and_Slot_Mapping_Integrity/
│⠀⠀⠀├── 4.1_Master_Cabinet_Boundary_Slot_Addressing/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Select the first slot (01), the final Master cabinet slot (46), and mid-shelf boundary slots on the touchscreen, confirming the displayed slot index and price match the physical coil label.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test wide/coupled twin-spiral slots (such as multi-coil snack bays) to verify that selecting the single logical slot actuates both linked motors synchronously without double-charging the cart.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Logical UI slot IDs map 1:1 to physical VMC motor indices; coupled coils execute as a single atomic vend command at the listed unit price.
│⠀⠀⠀│
│⠀⠀⠀├── 4.2_Slave_Cabinet_CrossBus_Slot_Addressing/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Select slots assigned to the right-hand Slave expansion cabinet and verify price accuracy, availability status, and cross-bus cabinet routing.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Alternate rapidly between selecting a Master cabinet slot and a Slave cabinet slot to test RS-485/CAN bus cabinet-ID switching latency and state retention.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Cross-cabinet slot commands include explicit cabinet-address headers; switching between Master and Slave items never misroutes a vend to the wrong cabinet's matching slot number.
│⠀⠀⠀│
│⠀⠀⠀├── 4.3_Mixed_Master_Slave_MultiItem_Cart_Sync/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Add multiple items spanning both the Master and Slave cabinets into Shopping Cart and verify itemized quantities, cabinet routing, and combined checkout execution.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Queue a mixed Master + Slave cart when the Slave cabinet door switch or drop sensor is in a simulated fault state to observe partial-vend handling.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Multi-cabinet carts execute sequential per-cabinet vend cycles with independent drop-sensor verification and automated partial-refund triggers if a secondary cabinet slot fails.
│⠀⠀⠀│
│⠀⠀⠀├── 4.4_ZeroStock_and_Disabled_Slot_Selection_Block/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Tap empty, sold-out, or technician-disabled coil positions on the item grid to confirm they cannot be added to the cart or purchased.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Add an item with exactly 1 physical unit remaining in stock, navigate back to Home, and attempt to select that same slot a second time before checkout.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Sold-out and fault-locked slots are non-selectable at both the UI layer and the VMC pre-vend validation check; cart reservation decrements available UI stock immediately.
│⠀⠀⠀│
│⠀⠀⠀├── 4.5_Cart_MaxCapacity_Overflow_Handling/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Repeatedly add items to Shopping Cart until reaching and exceeding the kiosk's maximum per-transaction item cap (typically 3–5 items to prevent delivery chute congestion).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Combine large-volume bottles with tall cans up to the cart limit to verify whether physical chute capacity rules prevent jamming the one-way anti-theft baffle.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Cart enforces a strict maximum item ceiling with a clear user notification, preventing multi-item chute pileups that could prop open the PUSH delivery flap.
│⠀⠀⠀│
│⠀⠀⠀├── 4.6_Rapid_Add_Remove_Total_Recalculation_Parity/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Rapidly tap +, -, and Remove controls inside Shopping Cart while auditing line-item subtotals, tax/GST calculations, and final payable totals.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Tap Remove on the final remaining cart item simultaneously with tapping the Checkout button to test for stale-total or $0.00 checkout transitions.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Cart total recalculates synchronously on a single thread; removing the last item immediately disables Checkout and clears any pending payment request.
│⠀⠀⠀│
│⠀⠀⠀├── 4.7_Category_Sort_Filter_Slot_Index_Consistency/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Apply category filters under the Sort tab (e.g., Drinks, Snacks, Confectionery) and select filtered items to confirm underlying slot IDs and prices do not shift to positional grid indices.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Add an item while a category filter is active, switch back to Home (unfiltered view), and verify that the exact physical slot number and price persist in the cart.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Product tiles bind directly to immutable slot-ID objects rather than relative RecyclerView/GridView adapter positions.
│⠀⠀⠀│
│⠀⠀⠀├── 4.8_Pagination_Previous_Next_State_Persistence/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Select items on Page 1, tap Next to navigate to subsequent slot pages, add additional items, and return via Previous to confirm cart state and UI badges remain intact.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Burst-tap Next at the final page and Previous on Page 1 to verify page-index bounds checking does not expose unconfigured or phantom slots.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Pagination boundaries clamp cleanly at [1..maxPages]; cart state persists globally across page transitions without duplicating or dropping selections.
│⠀⠀⠀│
│⠀⠀⠀└── 4.9_Promo_Code_and_Discount_Input_Validation/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: Where voucher, promo, or staff-discount redemption is exposed on the touchscreen, test expired codes, already-redeemed codes, and malformed strings.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: Apply a fixed-value discount exceeding the cart subtotal (e.g., $5.00 voucher on a $2.50 drink) to verify price-floor clamping and minimum card-authorization rules.
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: Discount validation occurs server-side with atomic single-use locks; payable totals clamp cleanly at $0.00 without integer underflow or negative-balance anomalies.
│
├── 05_Session_Timers_and_Payment_State_Sync/
│⠀⠀⠀├── 5.1_Countdown_Expiry_During_Card_Tap_Handshake/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Allow the 0:59 session countdown timer to reach 0:01–0:00 at the exact moment a contactless card or mobile wallet is tapped on the Nayax VPOS Touch.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Observe whether an MDB VEND_APPROVED frame arriving milliseconds after the UI resets to Home either completes the paid vend or immediately issues an MDB VEND_FAILURE reversal.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: UI session timer and MDB cashless session are synchronized; an expired UI session either cancels the MDB terminal before card read or atomically reverses any late authorization.
│⠀⠀⠀│
│⠀⠀⠀├── 5.2_Manual_Cancel_During_MDB_Authorization/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Tap Cancel or Back on the touchscreen immediately after presenting a contactless card while the terminal displays Authorizing / Processing.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test whether UI cancellation transmits an MDB SESSION_CANCEL command prior to VMC motor actuation, preventing a state where the card is billed without dispensing or vice versa.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Once card tap is detected and VEND_REQUEST is in flight, the UI Cancel button locks until the VMC receives a definitive VEND_APPROVED or VEND_DENIED response.
│⠀⠀⠀│
│⠀⠀⠀├── 5.3_Back_Navigation_Mid_Payment_Escrow_Reset/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Initiate checkout to wake the payment peripherals, then navigate back to Shopping Cart to add or remove an item before re-entering checkout.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Present a card immediately upon re-entering checkout to confirm the Nayax terminal displays the updated cart total rather than the cached prior-session amount.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Exiting the payment modal sends an explicit MDB session-cancel/reset sequence, forcing a fresh VEND_REQUEST with the updated price upon re-entry.
│⠀⠀⠀│
│⠀⠀⠀├── 5.4_ZeroDollar_and_Negative_Total_Checkout_Guard/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Attempt to trigger the Checkout flow when the cart is empty, when an unpriced ($0.00) slot is selected, or after rapid item deletion.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify that the VMC firmware independently rejects any serial CMD_VEND_SLOT packet lacking a valid MDB credit escrow or authenticated technician token.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Zero-value customer checkouts are blocked in UI logic and rejected at the VMC serial protocol layer.
│⠀⠀⠀│
│⠀⠀⠀├── 5.5_Partial_Cash_Insertion_Plus_Touch_Cancel/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Where coin or banknote acceptors are active, insert partial funds below the item price and tap Cancel or press the physical coin-return lever.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm that cancelling returns escrowed coins/notes and immediately zeroes the UI credit counter so residual credit cannot be spent by a subsequent user.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Escrow return is atomic with UI balance reset; cancelled sessions leave $0.00 residual credit on screen and in VMC registers.
│⠀⠀⠀│
│⠀⠀⠀├── 5.6_Repeated_Checkout_Button_Tap_Idempotency/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Rapidly multi-tap the Confirm / Pay button during the transition from Shopping Cart to the payment prompt.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify via terminal screen behavior and transaction receipts that only a single MDB VEND_REQUEST is issued per checkout attempt.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Checkout submission is protected by an idempotency state lock; duplicate taps do not queue double card charges or duplicate coil rotations.
│⠀⠀⠀│
│⠀⠀⠀├── 5.7_Payment_Timeout_Screen_Transition_Lock/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Let the payment screen time out without presenting payment, tapping the screen continuously during the timeout dismissal animation.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm that late asynchronous callbacks from the MDB serial bridge cannot fire after the UI returns to the idle Home state.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Every checkout transaction binds to a unique monotonic sessionId; callbacks matching an expired sessionId are discarded.
│⠀⠀⠀│
│⠀⠀⠀├── 5.8_PostVend_Receipt_QR_Screen_State_Isolation/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: During the post-vend dispensing animation and digital-receipt QR modal, tap underlying grid coordinates and bottom navigation tabs.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: For multi-item carts, verify the UI holds the dispensing lock until all queued coils complete rotation and drop verification before accepting new customer input.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Post-vend modal blocks new cart mutations until all queued motors finish cycling and the session closes cleanly.
│⠀⠀⠀│
│⠀⠀⠀└── 5.9_Offline_Network_Drop_During_Active_Checkout/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: Observe kiosk behavior when cloud connectivity drops (status pill transitions from Online to Offline) while a customer is on the payment screen.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: Confirm whether offline card authorization is disabled or strictly governed by Nayax VPOS offline risk limits without freezing the Android UI in an infinite loading spinner.
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: Network loss degrades gracefully within <=10 seconds, displaying a clear payment-unavailable prompt or controlled offline fallback without hanging the kiosk.
│
├── 06_WebView_Media_and_External_Intent_Containment/
│⠀⠀⠀├── 6.1_Help_Tab_Hyperlink_and_Mailto_Neutralization/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Open the Help tab and tap all visible phone numbers, support email addresses, website URLs, and interactive text elements.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test whether auto-linked text (android:autoLink) triggers an implicit ACTION_DIAL, ACTION_SENDTO, or ACTION_VIEW intent or spawns an Android "Open with" resolver dialog.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: All contact details are rendered as non-clickable static text; external intent resolution is blocked by Device Owner package restrictions.
│⠀⠀⠀│
│⠀⠀⠀├── 6.2_QR_Code_Modal_LongPress_Intent_Blocking/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Open any on-screen QR modal (such as e-receipt, support, or promotional QR popups) and perform long-press, double-tap, and drag gestures on the QR image.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify that QR codes are generated locally as static Bitmap/ImageView assets rather than loaded inside an interactive WebView.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: QR graphics accept zero touch intents beyond closing the modal; no browser preview or share sheet can be invoked.
│⠀⠀⠀│
│⠀⠀⠀├── 6.3_Text_Selection_Copy_Share_WebSearch_Suppression/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Perform sustained press-and-hold and rapid double-tap gestures across product titles, prices, error messages, and Help instructions.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm Android's floating text-selection action bar (Copy, Share, Select all, Web Search) is suppressed so Web Search cannot pivot into Google Search or AOSP Browser.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: textIsSelectable is false across all native views, and ActionMode selection menus are globally suppressed.
│⠀⠀⠀│
│⠀⠀⠀├── 6.4_Idle_Ad_Carousel_Touch_Interrupt_Sanitization/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Tap, swipe, and long-press across full-screen idle promotional banners and attract-loop slides to verify clean return to the Home product grid.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test tapping corners or embedded CTA graphics on cloud-pushed ad creatives to ensure remote media assets cannot carry clickable external redirect links.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Any touch on the idle attract screen strictly dismisses the screensaver to Home without evaluating embedded URLs or ad click-through intents.
│⠀⠀⠀│
│⠀⠀⠀├── 6.5_Video_Player_Controls_and_Fullscreen_Lock/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: During video ad playback or instructional video playback in Help, tap and double-tap the video frame to check for native MediaController or ExoPlayer UI controls.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Inspect for exposed scrubber bars, playback-speed menus, subtitle settings, or Cast buttons that could launch Android display/network settings.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Video playback runs in a chromeless SurfaceView/TextureView with all media transport and cast controls disabled.
│⠀⠀⠀│
│⠀⠀⠀├── 6.6_Embedded_WebView_URL_Redirect_Allowlisting/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Where any customer flow uses an embedded WebView (e.g., feedback form, digital receipt, or terms page), tap every header, footer, logo, and language link to test navigation boundaries.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Probe for third-party OAuth widgets, social media icons, or search bars inside hosted pages that could allow escaping to an open web browser session.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: WebViewClient.shouldOverrideUrlLoading() enforces a strict domain allowlist, blocking all external navigation and rejecting file://, content://, and intent:// schemes.
│⠀⠀⠀│
│⠀⠀⠀├── 6.7_SSL_Error_Dialog_Proceed_Button_Suppression/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Observe WebView behavior when a hosted page encounters an expired TLS certificate, clock-skew validation error, or venue captive-portal redirect.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm WebViewClient.onReceivedSslError() calls handler.cancel() silently rather than presenting a user-clickable warning dialog or captive-portal login prompt.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: TLS errors fail closed to a local static fallback view with zero interactive browser dialogs exposed to the user.
│⠀⠀⠀│
│⠀⠀⠀├── 6.8_Download_Manager_and_APK_Install_Prompt_Block/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Tap any document, catalog, or media asset links within Help or promotional views to verify that Android's DownloadManager cannot be triggered via touch.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm WebView.setDownloadListener() is overridden to drop all download requests and that INSTALL_PACKAGES / unknown-sources prompts are blocked by Device Owner policy.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: User-initiated file downloads are disabled at the WebView and OS policy layers; no download notifications or package-installer prompts can appear.
│⠀⠀⠀│
│⠀⠀⠀└── 6.9_PDF_or_Terms_Viewer_Print_Share_Isolation/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: If an allergen guide, nutritional sheet, or terms-of-service document viewer is accessible, audit its UI controls for Print, Share, Save, or Open with icons.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: Specifically verify that the Android Print Spooler (Add printer -> Wi-Fi Direct / Settings escalation path) cannot be invoked from any document view.
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: Informational documents are rendered as static bitmaps or sanitized in-app views with Print Spooler and Share intents completely disabled.
│
├── 07_Virtual_Keyboard_IME_and_Text_Input_Hardening/
│⠀⠀⠀├── 7.1_IME_Globe_and_Language_Switch_Key_Removal/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Trigger the soft keyboard on any customer-facing input field (e.g., e-receipt email/SMS, pickup code, promo voucher, or search bar) and inspect for the globe icon, language-switch key, or spacebar long-press IME picker.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Long-press the comma, period, and spacebar keys across both alphabetic and numeric keypad modes to test whether Android's "Change keyboard" system dialog can be summoned.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Kiosk uses an isolated custom in-app keypad or hardened single-locale IME with InputMethodSubtype switching disabled by Device Owner policy (setPermittedInputMethods).
│⠀⠀⠀│
│⠀⠀⠀├── 7.2_Keyboard_Settings_Gear_and_VoiceInput_Block/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Inspect the IME suggestion strip and symbol layers for a settings gear icon, microphone/voice-typing button, or emoji-picker settings shortcut.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test long-pressing keys on the top row or suggestion strip to verify that neither Android IME Preferences nor Google Voice Typing permission prompts can launch over the kiosk.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Settings gear, voice-input triggers, and third-party keyboard toolbars are stripped (EditorInfo.IME_FLAG_NO_PERSONALIZED_LEARNING and policy-restricted IME configuration).
│⠀⠀⠀│
│⠀⠀⠀├── 7.3_Clipboard_History_and_Paste_Buffer_Isolation/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Enter sample text into an input field, long-press or tap the cursor handle to check for Paste / Clipboard popups, and allow the session to reset before opening the same field as a subsequent user.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify whether AOSP/Gboard clipboard history trays retain prior customers' phone numbers, email addresses, or voucher codes across session timeouts.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Selection/paste action menus are disabled on input fields, and the system ClipboardManager buffer is explicitly wiped on every session reset.
│⠀⠀⠀│
│⠀⠀⠀├── 7.4_Autofill_and_Credential_Suggestion_Suppression/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Tap into text fields (especially email, phone, or numeric code inputs) and observe whether Android's Autofill framework renders saved-credential dropdowns or "Manage passwords" links.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test whether tapping an autofill suggestion chip pivots into Android Credential/Autofill Settings.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: android:importantForAutofill="noExcludeDescendants" is set on the root activity layout and Autofill services are disabled at the OS policy level.
│⠀⠀⠀│
│⠀⠀⠀├── 7.5_Special_Character_and_Control_Byte_Sanitization/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Submit non-alphanumeric payloads—including quotes, semicolons, angle brackets, backslashes, null-byte representations, and newline characters—into every exposed text or code field.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test whether pasted or multi-line strings containing \r\n or hex-delimiter sequences cause log injection or malformed JSON/serial framing when transmitted to cloud telemetry or local logs.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Input fields enforce strict character allowlists matching their business domain (e.g., [A-Z0-9] for pickup codes) and sanitize control characters prior to serialization.
│⠀⠀⠀│
│⠀⠀⠀├── 7.6_Oversized_String_Buffer_Truncation_Handling/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Hold down keys or repeatedly tap characters in text/numeric inputs to exceed typical field lengths (testing 256, 1,024, and 4,096+ characters).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Observe whether oversized strings cause horizontal layout overflow that pushes Submit or Cancel buttons off the 1080px portrait viewport or triggers an OutOfMemoryError / UI freeze.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Every EditText enforces an explicit android:maxLength filter and single-line clipping without distorting surrounding modal buttons.
│⠀⠀⠀│
│⠀⠀⠀├── 7.7_Local_Query_and_Delimiter_Input_Escaping/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: If the kiosk provides a product search bar or voucher lookup field, submit wildcard characters (%, _, *), SQL/JSON delimiters (', ", {, }), and path-traversal sequences (../).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test rapid sequential submissions of malformed search queries while toggling Sort category tabs to check for uncaught database or parser exceptions.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Local SQLite/Room queries use strictly parameterized bindings, and malformed queries return an empty result state without throwing UI error dialogs.
│⠀⠀⠀│
│⠀⠀⠀├── 7.8_Emoji_and_Surrogate_Pair_Rendering_Stability/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Where emoji or extended Unicode planes are reachable on the IME, input multi-byte UTF-16 surrogate pairs, zero-width joiners (ZWJ sequences), and right-to-left (RTL) override characters.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify that RTL override characters (U+202E) do not invert price displays or button labels, and that complex ZWJ glyphs do not crash legacy Android 7.1/9 Typeface rendering.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Non-ASCII symbol planes are excluded from customer input filters, and text rendering strips bidirectional control characters.
│⠀⠀⠀│
│⠀⠀⠀└── 7.9_Hardware_Key_Event_Emulation_via_IME/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: Audit any custom on-screen keypad or IME symbol layer for directional arrows (DPAD), Tab, Esc, Home, or Menu soft-keys that dispatch raw Android KeyEvent codes.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: Use Tab or directional soft-keys (if present) to test whether focus traversal can escape a modal dialog onto hidden background controls behind the scrim.
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: On-screen keypads emit direct character callbacks rather than raw system KeyEvent navigation codes, and modal focus traps prevent background traversal.
│
├── 08_Accessibility_and_Assistive_Overlay_Controls/
│⠀⠀⠀├── 8.1_Volume_or_Screen_Accessibility_Shortcut_Block/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Probe screen edges, hardware bezel seams, and boot/wake transitions for any exposed Android Accessibility Shortcut confirmation prompts or persistent accessibility triggers.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify that Device Owner policy sets DISALLOW_CONFIG_ACCESSIBILITY and clears enabled_accessibility_services so no third-party accessibility service can bind an overlay.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Accessibility shortcut triggers are disabled at the system policy layer; no system accessibility consent dialog can be invoked.
│⠀⠀⠀│
│⠀⠀⠀├── 8.2_TripleTap_Screen_Magnification_Gesture_Lock/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Perform rapid triple-taps (and triple-tap-and-hold gestures) across the idle screen, item grid, and checkout modal to test if Android Screen Magnification activates.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm that triple-tapping a product card neither zooms the viewport into a panned corner (stranding the user away from Cancel/Checkout) nor draws an orange magnification border.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: accessibility_display_magnification_enabled is locked to 0; rapid triple-taps are handled strictly by app-level debounce logic.
│⠀⠀⠀│
│⠀⠀⠀├── 8.3_TwoFinger_Hold_TalkBack_Activation_Check/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Place two fingers spaced ~5cm apart on the display and hold continuously for 5–10 seconds across idle and active states to test for AOSP TalkBack gesture activation.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test two-finger sustained hold immediately after an app relaunch or boot-up when AOSP setup/launcher fallbacks sometimes listen for assistive activation chords.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Two-finger hold gestures do not enable TalkBack spoken-feedback mode or alter single-tap touch semantics into double-tap-to-activate exploration mode.
│⠀⠀⠀│
│⠀⠀⠀├── 8.4_Accessibility_Floating_Button_Suppression/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Inspect the bottom navigation zone and right-hand screen margin for any translucent floating accessibility button (TYPE_ACCESSIBILITY_OVERLAY) or vendor assistive touch ball.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Specifically check Rockchip/Allwinner vendor ROMs where a floating "Assistive Touch" / "Suspend Button" overlay is enabled by default in factory firmware builds.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Floating accessibility buttons and vendor assistive-ball overlays are completely disabled in the production system image.
│⠀⠀⠀│
│⠀⠀⠀├── 8.5_HighContrast_and_FontScale_Layout_Overflow/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Audit typography and button bounds across all screens (including long product names and multi-item cart lists) for clipped labels, overlapping hitboxes, or off-screen action buttons.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify that the kiosk application overrides system Configuration.fontScale and display density scaling so remote or OS-level accessibility font changes cannot break button reachability.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Kiosk enforces fixed dp/sp scaling overrides; Home, Sort, Shopping Cart, Help, Cancel, and Checkout remain unobstructed at all times.
│⠀⠀⠀│
│⠀⠀⠀├── 8.6_SelectToSpeak_Overlay_Menu_Containment/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Verify that no Select-to-Speak floating play/stop toolbar can be toggled or dragged onto the kiosk screen.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm that if any accessibility service is permitted for ADA/DDA compliance, its overlay panel contains zero settings gears, tutorial links, or external intent triggers.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Unapproved accessibility overlays are blocked; any mandated assistive UI runs strictly within an isolated, intent-stripped kiosk sandbox.
│⠀⠀⠀│
│⠀⠀⠀├── 8.7_Switch_Access_and_Focus_Traversal_Isolation/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Observe whether touching screen edges or performing rhythmic tap-and-hold sequences initiates auto-scanning focus highlights across UI elements.
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Confirm non-interactive background elements and hidden off-screen tabs have android:focusable="false" and importantForAccessibility="no" so focus rings cannot highlight disabled controls.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Switch Access scanning is disabled, and focusable view hierarchies are restricted strictly to active foreground controls.
│⠀⠀⠀│
│⠀⠀⠀├── 8.8_Assistive_Menu_Screenshot_and_Home_Action_Block/
│⠀⠀⠀│⠀⠀⠀├── Test_Scenario: If a vendor assistive menu or accessibility panel is present on the build, audit every action icon inside the menu (e.g., Home, Back, Recents, Notifications, Screenshot, Power).
│⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Verify that triggering Home or Recents from an assistive overlay cannot bypass LockTask pinning to expose the AOSP desktop.
│⠀⠀⠀│⠀⠀⠀└── Expected_Defense: System assistive menus are disabled; LockTask policy blocks Home, Recents, Notifications, and Screenshot actions across all input sources.
│⠀⠀⠀│
│⠀⠀⠀└── 8.9_Audio_Feedback_and_TTS_Engine_Settings_Block/
│⠀⠀⠀⠀⠀⠀├── Test_Scenario: Trigger audio prompts (button clicks, checkout chimes, voice guidance) and verify no volume slider overlay (AudioManager system UI) appears with a settings expansion icon.
│⠀⠀⠀⠀⠀⠀├── Niche_Variations: Ensure that if a Text-to-Speech (TTS) engine fails or lacks a voice pack, the OS suppresses the "Install voice data" / TTS Settings prompt rather than rendering a clickable dialog.
│⠀⠀⠀⠀⠀⠀└── Expected_Defense: System volume HUDs and TTS voice-data installation intents are suppressed; audio playback fails silently if an asset is missing.
│
└── 09_Fault_Recovery_Error_Modals_and_Telemetry_States/
⠀⠀⠀⠀├── 9.1_DropSensor_Fault_Modal_Dismissal_Lock/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Observe kiosk UI behavior when an infrared drop-sensor anomaly or "Item not detected" alert appears during a vend cycle, testing tap responsiveness on the alert modal.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Rapidly tap behind and around the fault modal to ensure the user cannot trigger a second unpaid coil rotation or stack multiple refund prompts before the VMC completes fault recovery.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Fault modals are strictly modal, serialize hardware recovery states, and cap automated retry/refund sequences atomically.
⠀⠀⠀⠀│
⠀⠀⠀⠀├── 9.2_VMC_Serial_Disconnect_Banner_Touch_Behavior/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: When the Android host loses UART/RS-232 heartbeat with the VMC board (simulated in lab or observed during controller reset), audit the resulting "Out of Service" / communication-error overlay.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Tap across the underlying product grid during VMC disconnection to confirm items cannot be added to the cart or sent to the Nayax payment terminal while the VMC is unreachable.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Loss of VMC serial heartbeat immediately locks all customer selection and payment triggers until two-way VMC status polling succeeds.
⠀⠀⠀⠀│
⠀⠀⠀⠀├── 9.3_Motor_Jam_Slot_Lockout_UI_Enforcement/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: When a spiral coil reports an over-current/jam fault (FAULT_MOTOR_JAM), verify the affected slot immediately transitions to an unavailable state on the touchscreen.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Switch between Home, Sort category tabs, and Next/Previous pages to confirm the faulted slot state persists across all UI views and cannot be re-added via cached tiles.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Faulted slot flags are stored in a central state store shared across all grid adapters and validated again prior to payment initiation.
⠀⠀⠀⠀│
⠀⠀⠀⠀├── 9.4_Temperature_OutOfRange_HealthLock_Bypass_Check/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: When the refrigerated cabinet exceeds safe temperature thresholds (triggering a health-safety lockout on perishable slots), attempt to select locked slots via rapid taps or category filters.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Test tapping perishable slots immediately after a UI refresh or screensaver dismissal to confirm health-lock enforcement does not suffer from a startup polling race condition.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Perishable slots remain locked out until VMC temperature telemetry reports sustained compliance within safe operating bounds.
⠀⠀⠀⠀│
⠀⠀⠀⠀├── 9.5_Bill_Validator_Full_or_Jam_State_UI_Handling/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: When the ITL banknote acceptor reports stacker-full, jam, or disabled status over MDB, verify the checkout screen updates accepted payment methods accurately.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Attempt to initiate a cash checkout when only cashless (Nayax) is healthy, confirming the UI guides the user cleanly without hanging on an unresponsive bill acceptor.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Peripheral health states dynamically update checkout UI options and prevent dead-end payment states.
⠀⠀⠀⠀│
⠀⠀⠀⠀├── 9.6_Nayax_Terminal_Offline_Fallback_Selection/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Observe touchscreen checkout behavior when the Nayax VPOS Touch displays Out of Service, Updating, or cellular link loss during a customer session.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Rapidly tap Pay by Card while the Nayax terminal is rebooting or offline to verify the kiosk fails gracefully back to Shopping Cart or cash-only mode without freezing.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: MDB cashless readiness is checked prior to entering card checkout; an unready terminal aborts the card request cleanly within <=5 seconds.
⠀⠀⠀⠀│
⠀⠀⠀⠀├── 9.7_App_Crash_AutoRelaunch_Window_Exposure/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: During any automated watchdog restart or cold boot of the vending APK, continuously tap the screen edges and center to test whether the underlying AOSP launcher or status bar is reachable during the transition window.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Measure the exact recovery latency between process termination and full LockTask restoration.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Kiosk runs as the sole custom HOME activity with a black/branded splash theme and persistent LockTask binding, exposing zero AOSP UI during restarts.
⠀⠀⠀⠀│
⠀⠀⠀⠀├── 9.8_OTA_Update_Progress_Overlay_Touch_Blocking/
⠀⠀⠀⠀│⠀⠀⠀├── Test_Scenario: Observe kiosk touch behavior during scheduled cloud OTA APK updates, price-table syncs, or ad-media downloads.
⠀⠀⠀⠀│⠀⠀⠀├── Niche_Variations: Tap across the screen during APK installation or reboot prompts to verify that Android's system package-installer progress bar exposes no Cancel button or launcher fallback.
⠀⠀⠀⠀│⠀⠀⠀└── Expected_Defense: Silent Device Owner package installation (PackageInstaller) executes behind a full-screen non-interactive maintenance overlay with zero user-cancelable system dialogs.
⠀⠀⠀⠀│
⠀⠀⠀⠀└── 9.9_Clock_Drift_and_Session_Timestamp_Display_Audit/
⠀⠀⠀⠀⠀⠀⠀⠀├── Test_Scenario: Inspect any on-screen clock, session countdown (0:59), and generated e-receipt timestamps for accuracy and monotonic behavior.
⠀⠀⠀⠀⠀⠀⠀⠀├── Niche_Variations: Verify that session timers use SystemClock.elapsedRealtime() rather than wall-clock System.currentTimeMillis() so NTP clock adjustments mid-session cannot prematurely expire or stall a payment countdown.
⠀⠀⠀⠀⠀⠀⠀⠀└── Expected_Defense: All UI session timers rely on monotonic uptime clocks, while TLS/cloud telemetry maintains accurate NTP synchronization.

`
