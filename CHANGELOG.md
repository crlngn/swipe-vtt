# Changelog

All notable changes to Swipe VTT will be documented in this file.


## [2.7.1] - 2026-09-05

### Added

- **Per-actor "Disable Swipe mobile sheet".** The actor directory context menu can exclude an actor from the mobile drawer. Flagged actors open the system's own sheet on mobile at every entry point (directory, token double-tap, sheet interception) and are left out of the avatar carousel.
- **Touch dragging for Foundry `Draggable` handles.** HUDs and frameless apps from other modules (e.g. Calendaria) that drag with Foundry's `Draggable` can now be dragged with a finger; the browser no longer steals the gesture for panning.
- **Item Piles compatibility**: merchant, inventory, settings and text-editor windows are pinned to their desktop sizes and scaled to fit, instead of squishing.

### Changed

- **Windows scale at their natural size.** Module windows with no min-width used to be clamped to the phone width by Foundry/TyphonJS and render squished. Swipe now restores the size the application declares (both dimensions) before scaling it down, unless a stylesheet min-width already forces scaling.
- **dnd5e dialogs** (roll configuration, activity usage, rests) take the same 500px min-width as other windows and scale down, keeping their desktop proportions at the larger mobile font scale.
- **Settings windows on small devices**: taller inputs (2.75rem) for tapping; form groups wrap with wide labels so buttons, selects, range pickers and inputs sit on their own row; Game Settings gets a taller category sidebar, roomier groups and spacing; "Open Game Settings" moved to the top of Swipe's General tab. Overrides hold when Carolingian UI is active.
- **Calendaria HUD** is hidden in mobile mode.

### Fixed

- Foundry ApplicationV2 windows were never found by the window scaler (string ids), so their position was never synced; scaled dnd5e dialogs also landed half off-screen because Foundry rewrote the position after Swipe set it.
- Windows that fit the viewport re-checked their size every 150ms forever.
- `module-compat.css` was never bundled; its Token Action HUD rules are now live.

## [2.7.0] - 2026-09-01

### Added

- **PF2e standalone support.** The proxy-hosted standalone client now works for PF2e worlds: the GM ships derived stats (saves, skills, perception, AC/HP/dying, hero points, senses, identity, coins) as serialized data, and the client rebuilds the PF2e actor shape with working **check rolls** (saves/skills/perception/initiative via the GM, single-d20 roll dialog with no advantage row). The **condition grid** applies/removes conditions from the phone, **currency is editable**, and **Standalone appears in the performance-mode dialog** for PF2e. Strikes and spellcasting are the remaining phase.
- **The standalone client is an installable PWA** — web-app manifest with the Carolingian icon, offline-capable app shell, and "Add to Home Screen" launches that restore the last session automatically.
- **The dnd5e damage tray works on standalone** — styled like in Foundry, with collapse, per-target multipliers, and Apply relayed to the GM.
- **Standalone infrastructure**: the GM snapshots system CONFIG (labels, status effects, PF2e conditions) into the boot payload; owned-item CRUD is relayed live in both directions; module templates/assets are mirrored for the production proxy (fixing template/icon 404s for every system); system stylesheets are bundled; inline enricher codes (@UUID/@Check/@Damage/@Localize, inline rolls) render as readable chips; the GM bridge starts as soon as Patreon is connected mid-session; presence clears immediately when the page closes.
- **Mobile-styled confirmation dialog** replaces Foundry's native confirm for item and intercession deletes.
- **Divine intercessions can be removed** from the PF2e Effects tab (with confirmation), and effects/intercessions render on standalone.

### Fixed

- **"Disable Dice So Nice" reliably disables it.** DSN initializes asynchronously, so the toggle silently missed on slow devices and never re-applied after a reload; it now defers to DSN's ready hook. **"Disable Heavy FX Modules" actually works** — it had no consumer at all; it now drives FXMaster's per-client switch.
- The PF2e Effects tab no longer duplicates every active condition below the grid — the detail list only shows conditions with a value or duration.
- Container contents' quantity inputs, intercession row alignment, and inline content-link chips styled correctly.
- Local development: the proxy's auth bypass now covers world-token minting, so standalone can be provisioned and tested locally.

## [2.6.0] - 2026-08-30

### Added

- **Mobile chat is now free.** The chat drawer — one message at a time with swipe navigation — is available to everyone, not just patrons.
- **Type from mobile.** A keyboard button (bottom-left, shown while the chat drawer is open) reveals Foundry's native chat input full-width and focuses it. Sending a message drops the input and switches back to the messages. The editor toolbar (Format/Insert Image/…) is hidden on phones where it doesn't fit.
- **Add items to the PF2e inventory.** An **Add Item** button opens a searchable, tappable equipment picker (PF2e's own index): multi-select with an accent outline, a per-row quantity (default 1), long-press to open an item's sheet, and **Done** adds the whole selection.
- **Use PF2e consumables.** Consumable rows (scrolls, potions, elixirs, wands, …) get a **Use** button that runs the system's `consume()` — scrolls cast their spell, others post their activation card, and charges/quantity are tracked automatically.

### Changed

- A valid world token now covers a second GM without requiring their own Patreon login — the reconnect prompt only appears when premium is genuinely unavailable.

### Fixed

- The Dice Tray module no longer pops the mobile keyboard (and shifts the layout) on every die tap inside the chat drawer.
- Taps now pass through the floating button stack to the chat input and Roll button behind it while chat is open.
- The `#flash-rolls-icon` is hidden on mobile, where its menu can't open.
- Softened crlngn-ui's harsh white whisper-message border on mobile.
- Inventory currency chips use the tertiary background.

## [2.5.0] - 2026-08-25

### Added

- **PF2e Party sheet (free).** The party actor gets a mobile sheet with three tabs — **Overview** (member roster with avatar, class, HP and AC), **Exploration** (travel-speed summary with Rest and Roll-Initiative actions, plus each member's speed, perception and exploration activity), and **Stash** (the party's shared inventory with editable quantities). The party actor also appears in the avatar carousel.
- **PF2e familiar support on the mobile sheet.** Familiars previously opened an empty sheet; they now show a **Character** tab (AC and Dying, with the master's name and spellcasting attribute in place of the wounded/initiative boxes familiars don't have), plus **Actions** (familiar abilities) and **Proficiencies** (skills). No Spells tab — familiars can't cast.
- **PF2e linked ammunition for reload-0 weapons** (bows, slings): the selected ammunition can be picked directly on the strike.

### Changed

- **PF2e damage absorbs temporary HP first.** Applying damage from the mobile HP dialog now routes through the system's own damage application, so temp HP (and a raised shield) is consumed before real HP.
- **The HP dialog stays open and updates in place.** Heal, Damage and Temp-HP changes now refresh the dialog's current/temp readout immediately instead of requiring you to close and reopen it.

### Fixed

- **Changing a member no longer hijacks the drawer to the party sheet.** An incidental re-render of a party/group actor (e.g. changing a member's ammunition) could open or switch the mobile drawer to the party sheet even when it was never opened; the drawer now only opens on an explicit, user-initiated render.
- The party/group sheet now refreshes when a member changes while it is already open.
- PF2e **Dying/Wounded pips** show their filled colour when tapped (a base rule was outspecifying them).
- The temp-HP **shield icon and `+N` value** now use the same accent colour as the temp segment of the HP bar instead of a fixed blue.
- The **HP dialog is reachable while a character is at 0 HP / dying**, so you can heal back up — a dying overlay was swallowing the tap.
- Removed the redundant **dying overlay** that covered the HP numbers in the drawer header; the interactive dying pips on the Character tab remain.

## [2.4.0] - 2026-08-22

### Added

- **PF2e action-option toggles on the mobile sheet.** The Actions → Encounter tab now shows an **Action Options** section exposing the weapon and class roll-option toggles (Hunt Prey, rogue debilitations, etc.), driven through PF2e's own `toggleRollOption` API. Value toggles get their dropdown; always-active ones show the dropdown only.
- **PF2e loaded ammunition and reload.** Ranged strikes that use loaded ammo (crossbows, firearms) show the currently loaded rounds with an **editable quantity**, plus a **Reload** aux-action that loads compatible ammo via the system's own `weapon.attach`. Reload auto-picks a single compatible ammo or opens a bottom-sheet picker; reloading an already-loaded weapon lets you swap ammo. Ammo changes update in place, so the expanded strike no longer collapses.
- **Graceful WebGL context-loss recovery on mobile.** When the browser drops the GPU context under memory pressure (common on phones), the game canvas no longer silently dies — an overlay explains what happened and offers a one-tap reload, for every system.

### Changed

- **iPhones default to Sheets-Only mode** until the player explicitly chooses a performance mode, avoiding heavy canvas loads on first run.
- **Performance-mode choice now follows the user, not the device.** It persists as a user flag (syncing across browsers and into the proxy-hosted standalone client via the GM relay) instead of per-browser local storage.
- **Standalone redirect is guarded.** Before sending a player to the standalone client, the module confirms with the proxy that the world is still registered, so a stale local world token no longer strands players on an error page; error screens gained a **Back to Foundry** button.
- Item descriptions on mobile sheets fade their bottom edge only when the text actually overflows, instead of always looking cut off.
- Larger default touch targets in the mobile sheet drawer.

### Fixed

- **D&D 5e activity dialogs are usable on phones again.** Non-attack activity dialogs (spell usage, Lay on Hands, rests, etc.) were rendering at desktop width, clipped and nearly untappable. All 5e dialogs now size correctly on mobile, and no longer freeze at the wrong size after being dragged or pinch-scaled.
- Silenced the Foundry V14 `Scene#templates` deprecation warning triggered by token double-tap and standalone scene sync (templates were merged into Regions in V14).
- The mobile sheet-interception guard was comparing minified class names and never matched in production builds; it now uses a stable marker.

### Internal

- Production builds no longer ship source maps (module maps are `hidden`; the standalone bundle emits none), and the release now fails hard if a map or `sourceMappingURL` slips into the package. A CC BY-NC-4.0 licence banner is embedded in both built bundles.

## [2.3.0] - 2026-06-26

### Fixed

- **Standalone reconnect leak.** Socket listeners are now bound once per client instead of accumulating on every reconnect.
- **Mobile-mode memory leaks** from stale event listeners, hooks, and a lingering FPS poll when leaving mobile mode.
- **MiniCanvas token-update rebuild storm** scoped and polls bounded; fixed a broken scene switch under `noCanvas`, and the mini-canvas now pans to the user's character token on scene change.
- **Swipe checkbox checkmarks** rendered correctly without Carolingian UI installed.
- Removed dead SafariCompat Sequencer iOS blend-fix code.

### Changed

- ImageOptimizer scene analysis parallelized and directory browsing de-duplicated for faster optimization.

## [2.2.0] - 2026-06-08

### Fixed

- Mini-canvas double-tap could open the sheets of actors the player doesn't own.

## [2.1.1] - 2026-06-05

### Fixed

- **Premium, Patreon auth, and the standalone client no longer break on LAN/localhost setups.** Dev mode was being inferred from the Foundry hostname, so any world reached over a local address (`localhost`, `192.168.x`, `10.x`, `172.16–31.x`, `*.local`) pointed premium validation, the "Connect with Patreon" / auth-code buttons, and the standalone redirect at the user's *own* machine on port 3847 — which runs no proxy, so the app hung on the loading screen and the auth links hit a dead localhost URL. Dev mode now derives only from the build flag, so production builds always use the hosted proxy.
- **Connect-phone QR now respects each user's mode.** The QR points at Foundry's native `/join` page by default and only links to the standalone client for users set to **Standalone** in Settings → Users (previously it always linked to standalone whenever a world token existed).

## [2.1.0] - 2026-06-04

### Added

- **Standalone mobile client restored on Foundry V14 — now proxy-hosted.** V14 broke the in-Foundry Standalone SPA (module HTML served as `text/plain` + socket.io gated behind httpOnly session cookies). The client is now hosted on the Carolingian proxy and reaches the world through a bridge instead of connecting to Foundry directly. The GM's Foundry module opens an outbound WebSocket bridge to the proxy; the proxy relays envelopes between the GM and each player's browser, keyed by world. The GM module remains the authority for all data and rolls; the proxy is a stateless router and socketlib stays intra-world. Phone connects by scanning the QR / opening a `?world=<worldId>` link.
- **GM approval flow for standalone joins.** When a player opens the standalone link, the GM gets a Join Approval prompt ("{n} user(s) joining from Standalone link") with Approve per request. Controlled by the world-scope **Standalone Approval Policy** setting: *prompt every time* (default), *auto-approve players I've approved before* (trusted), or *auto-approve everyone* (dev only). An inline **Auto-approve mobile connection requests** toggle on the approval dialog and a matching control in Settings → Users mirror the same policy.
- **Play tokens — persistent, GM-revocable standalone sessions.** Approved devices receive an HMAC-signed play token (signed with an auto-generated per-world secret) so a phone stays logged in across reconnects for ~14 days without re-approval. The active-token registry is world-scoped and verified at every player handshake.
- **Per-user password fast-path.** A GM can set an optional standalone password per user (hashed, stored world-side, never copied from the Foundry account); entering it skips the approval prompt entirely on join.
- **Disconnect standalone user.** A GM can revoke a user's standalone access from the user controls; active sessions are dropped ("Disconnected by GM" → redirect) and the device must be approved again to reconnect.
- **Standalone presence in the GM Players list.** Connected standalone players set `User#active`, so they show un-greyed in the GM's Players widget instead of appearing offline. (GM-client-only.)
- **Image relay with IndexedDB caching.** Scene, token, and actor images that the standalone client can't fetch directly (DDB/system assets) are relayed through the bridge on demand and cached in IndexedDB, intercepted before render so there are no broken-image 404s. Status-effect icons are pre-resolved.
- **Theme mirroring.** The standalone client mirrors the world's Swipe theme, defaulting to the crlngn-ui teal (`rgb(78,139,158)`).
- **Macro hotbar on standalone.** Players see, add, remove, and execute their hotbar macros; execution briefly drives the player's mini-canvas selection and restores the GM's selection afterward.
- **Font Awesome Free v6 in the standalone UI.** The standalone client no longer depends on FA Pro weight classes so it renders correctly without a Pro license.
- **Live document sync to the standalone client.** GM-side actor and active-effect changes — applying or clearing a condition, editing HP, adding/removing an effect — now relay to connected standalone players in real time instead of going stale until reconnect. A player's own condition toggles update instantly (optimistic) and reconcile against the GM's authoritative state. Only actors a player can see are relayed.
- **Offline (GM-offline) read-only access on standalone.** When the GM is offline, a player can still open their character read-only from the last session cached on the device; the session upgrades to live automatically when the GM reconnects.
- **Spell sections by casting method on mobile sheets.** The dnd5e mobile spellbook and the Combat tab now break always-available spells into At-Will / Innate / Ritual sections ahead of the leveled groups, matching the core sheet. The spellbook header also shows the prepared-spell count (`value/max`), excluding always-prepared spells and cantrips.
- **Standalone opens the expanded sheet layout on tablets by default.** On a tablet-width device the standalone client now defaults to the wide multi-column layout; the toggle in mobile settings still wins, and in-Foundry behaviour is unchanged.

### Changed

- **Supersedes the 2.0.0 "Standalone disabled on V14" limitation.** The QR Code dialog can again offer the Swipe standalone client on V14 (via the proxy bridge) alongside the native `/join` Mobile Profile flow.

### Fixed

- **Standalone condition highlights stay in sync.** Active conditions on the Effects tab no longer lose their selected state after a data refresh, and toggling a condition reflects immediately rather than reverting.
- **Standalone Combat tab action filtering.** Spells now appear under the correct action type — bonus-action spells such as Divine Smite were missing — by resolving activation the way dnd5e does (item casting time unless the activity overrides it). Feature and spell use counts (e.g. Lay On Hands `9/10`) now show.
- **Standalone labels no longer show raw localization keys** for feature types and classes when the relayed i18n snapshot lacks a translation.
- **Custom dice icons render on the dice bar** in both standalone and in-Foundry mobile, filling Font Awesome Free gaps.
- **Long token name labels stay centered** under the token on the mini-canvas.
- **Standalone mode is selectable again** in the user Performance Mode dialog and the GM Users-tab (it was disabled during the V14 work). Picking it now opens the proxy-hosted client instead of falling back to Sheet-Only, gated on the world having a valid proxy token.
- **Double-tapping a token in the standalone mini-canvas** opens its character sheet again (it errored instead of opening).

## [2.0.0]

### Breaking

- **Foundry V14+ required.** v2.x targets Foundry V14 exclusively (`compatibility.minimum: "14"`). V13 worlds will not auto-update to v2 — V13 users should stay on v1.22.x. Module ID is unchanged (`swipe-vtt`) so settings, flags, and premium auth survive the upgrade for users moving from V13 to V14.
- **Standalone client + phone-join page disabled on V14.** Foundry V14 serves module HTML files as `text/plain` (anti-XSS) and gates socket.io behind httpOnly session cookies, breaking both the previous Standalone SPA and the `phone-join.html` companion page. The QR Code feature now points at Foundry's native `/join` page instead. Standalone source remains in-tree for a future proxy-bridge implementation but is not loaded on V14.

### Added

- **Mobile Profile — paired user for phone login.** GMs can create a `(Swipe)` duplicate User per player so a phone can log into Foundry's native `/join` page without conflicting with the player's desktop session. The duplicate inherits role, assigned character, color, avatar, and permissions from the original, and is granted `OWNER` permission on every actor the original owns. Multiple sessions for the same player coexist (V14 allows it), so phone and desktop can both be live.
  - Passwordless by default; the GM can set a password via the QR dialog if the QR could be seen by others.
  - GM users can also be duplicated — the duplicate gets the `ASSISTANT` role rather than `GAMEMASTER` so the phone session doesn't act as a second full GM.
  - Bidirectional flag bookkeeping (`mobileDuplicateOf` on the duplicate, `mobileDuplicateId` on the original) with defensive orphan-flag repair if the back-reference is ever lost.
- **Auto-create on QR dialog open.** When the GM opens the Swipe QR Code dialog for a player who doesn't yet have a Mobile Profile, one is created automatically and the QR targets it. Controlled by the world-scope **Auto-Create Mobile Profile** setting; off by default for safety, can be enabled per-world.
- **Auto-resync of duplicate from original.** When the original user's role, character, color, avatar, or permissions change, the duplicate is auto-mirrored via the `updateUser` hook (active GM only, to avoid concurrent writes from multiple connected GMs). Hotbar, pronouns, and similar personalization are intentionally not synced so the phone can develop its own.
- **Auto-cleanup on user deletion.** Deleting a user via Foundry's User Management cascades correctly: deleting the original cascade-deletes the duplicate; deleting the duplicate clears the back-reference flag on the original. Active-GM-gated.
- **Manage Mobile Profile in Settings → Users tab.** Each non-duplicate user row has an Add Mobile Profile / Remove Mobile Profile button in its Performance Overrides section. `(Swipe)` users are filtered out of the user list so the GM sees one row per player.
- **Connect Phone QR dialog rework.** Simplified to a single QR + URL row when the duplicate is already present, plus a per-row Set Password / Add Mobile Profile button gated to GMs. The dialog now correctly targets the user being edited via the User Config (was previously falling back to the GM's own id).
- **#players widget integration.** The active-players widget hides `(Swipe)` rows when both sessions are inactive or only the original is connected, and appends a small mobile icon next to the player's name when the phone session is live. If only the phone is connected, the duplicate's row replaces the original in the list. The icon inherits the row's text color and follows whichever row is visible.

### Changed

- **QR code targets `/join`.** The Swipe QR Code dialog now encodes `{base}/join?user={id}&name={name}` (Foundry's native login page) instead of the broken-on-V14 `standalone.html` or `phone-join.html` paths. Player picks their `(Swipe)` username from the dropdown and joins; passwordless flow takes them straight to `/game`.
- **Manifest `compatibility.minimum` raised to `"14"`.** Foundry's auto-updater respects this — V13 worlds won't be offered v2 even if the package directory serves v2 as latest.



### Fixed
- **`Token#detectionModes` shape change on Foundry V14** — V14 switched detection modes from an `ArrayField` to a `TypedObjectField` keyed by mode id, so `(t.detectionModes ?? []).map(...)` threw `.map is not a function` when switching levels. Added `TokenCompat.getDetectionModes` to normalize the two shapes; applied to the standalone scene-packet builder, the standalone `createToken` broadcast, and the MiniCanvas sight-range / visibility computations.
- **Actor cache build threw on dnd5e 5.3+** — `details.race` and `details.background` became getter-only in dnd5e 5.3, breaking the standalone actor-cache builder. Now version-gated: dnd5e ≥ 5.3 shallow-clones `details` before mutating, older versions keep the direct-assignment path.

## [1.21.0]

### Added
- **Foundry V14 compatibility for scene image features** — V14 moved `Scene#background` and `Scene#foreground` onto an embedded `Level` document and emits a deprecation warning every time the legacy accessors are read. Image optimization, the optimized-image swap-in, and memory diagnostics now use a version-aware adapter (`SceneCompat`) that reads from `scene.firstLevel` on V14+ and the legacy fields on V13. Single-level scenes behave identically across versions.
- **Multi-level scene support for image optimization and memory tally on V14** — multi-level scenes (a V14-only feature) now have every Level's background/foreground analyzed by the optimizer dialog and counted in the texture-memory estimate. Per-level entries are labeled with the Level name (e.g., "Background (Upper Floor)") to disambiguate.

## [1.20.1]

### Fixed
- **Assistant GMs couldn't load premium bundles** — `socketlib.executeAsGM` short-circuits to a local handler when the caller's `isGM` flag is true, which in V13 includes Assistant GMs. The Assistant would dispatch the bundle request to themselves, fail the patron check, and end up with premium disabled. Bundle requests (and version-broadcast re-fetches) now route explicitly to the active primary GM.

## [1.20.0]

### Added
- **Wall geometry on Simplified Token Map** — a 60ft circular reveal around the player's selected (or last-dragged) token shows nearby wall lines, with a feathered/gradient outer edge. Closed and locked doors render distinct from solid walls; open doors render dashed.
- **Live door state propagation** — toggling a door open/closed/locked on the GM canvas updates the simplified map for connected players in real time (via `updateWall` hook in-Foundry, and a new socket broadcast for Standalone clients).
- **GM setting: "Show Walls on Simplified Token Map"** — world-scope toggle (default ON) under the GM-only section of the Swipe VTT settings dialog. Disable for theatre-of-the-mind scenes.
- **Secret door privacy** — secret doors (`door=SECRET`) and non-blocking walls (`move=NONE`) are filtered server-side before reaching player clients.
- **GM-offline blocks player movement** — if no GM is connected, MiniCanvas drags are rejected client-side with a "GM must be online" notification (in-Foundry and Standalone).

### Fixed
- **SocketUtil missed `socketlib.ready` hook** — on player clients where socketlib finished initialization before our module, `Hooks.once` never fired and `SocketUtil.socket` stayed null. Visibility relay, premium bundle requests, and the new movement validator silently no-op'd. Now registers synchronously when socketlib is already loaded.
- **Simplified Token Map selection wiped on token refresh** — `createTokens()` now snapshots and restores the previous selection and target state, so server-side token updates, drags, or the periodic sync no longer clear the player's active selection.
- **Wall radius followed wrong token after drag** — the dragged token now becomes the active selection at drop time, so the 60ft wall reveal centers on the last-moved token, not the player's main character.

## [1.19.2]

### Added
- **MiniCanvas wall collision check on player drags** — players can no longer drag tokens through scene walls on the Simplified Token Map. Drag commits are validated by the GM client via socketlib using Foundry's polygon backend (`CONFIG.Canvas.polygonBackends.move.testCollision`); blocked moves snap back with a notification. Honors closed/locked doors and one-way walls; open doors and `move=NONE` walls allow passage.

### Fixed
- **GM premium cache stale mid-session** — refresh the GM's premium cache during the session so players get the current bundles after the GM reconnects or refreshes Patreon status.

## [1.19.1]

### Changed
- **GM premium relay when Swipe disabled** — GMs with "Enable Swipe in this client" off now run the premium socket + session init only, so players can still validate premium through them. No mobile UI is loaded on the GM's client.

### Fixed
- **World-token fallback for fresh installs** — players whose GM is online but unresponsive (or returns a generic error) now fall back to the world token after the cache, closing the gap on fresh installs.

## [1.19.0]

### Added
- Toggle to disable Swipe in a specific client (per-user)
- GM / Assistant GM users now appear in the Swipe mode configuration in Settings
- QR code link for all players (shared by the GM)
- Touch-drag and window drag handler improvements

## [1.18.2]

### Fixed
- Macro hotbar drawer z-index when the sheet carousel is open
- Macro slot image expanding on long press

### Changed
- Macro hotbar button is now visible by default (`hideMacroButton` default: false)

## [1.18.1]

### Added
- **Inventory: Attune/Unattune toggle** — items with attunement show an attune button in expanded details
- **Inventory: Delete item** — remove button with confirmation dialog in expanded item details
- **Inventory: Add Item** — button to add items from the compendium browser (filtered to inventory types)
- **Macro hotbar drawer** — mobile-friendly macro hotbar with grid layout matching Foundry core style
  - Toggle button in button stack (hidden by default, enable in Settings > Controls)
  - Page navigation between hotbar pages
  - Long-press context menu: add, edit, remove macros
  - Macro search dialog for adding from world macros or compendium packs
  - Drag-and-drop to reorder or swap macro slots
  - Drag handle to dismiss drawer
- Fade mask on scrollable item descriptions in expanded details

### Fixed
- **TextureLoader deprecation** — use `foundry.canvas.TextureLoader` (Foundry V13+)
- **Senses deprecation** — read from `senses.ranges.*` for dnd5e 5.3+ compatibility
- **Window drag position sync** — close button no longer snaps window to original position after dragging
- **Dice bar positioning** — always appears above the dice button regardless of other buttons
- Activity name overflow in inventory — truncated with ellipsis
- Drawer handle touch targets increased for easier interaction

## [1.17.4]

### Added
- Auto-optimization for scenes via setting and improved optimizer prompt dialog
- Scene image check to warn when images exceed device max texture size
- Default scene image size threshold changed to 2048px

### Fixed
- Clean up premium loader notifications (use LogUtil, mobile-only reporting)

## [1.17.0]

### Added
- **MiniCanvas** — lightweight grid + token view for noCanvas mode
  - MiniCanvas enable/allow settings with opt-in prompt
  - MiniCanvas support for standalone mode
- Support delete templates via socket in standalone mode
- Send target token IDs with standalone roll requests

### Fixed
- Guard preventDefault with cancelable check in touch handlers
- Standalone MiniCanvas token undo

## [1.16.3 – 1.16.8]

### Fixed
- Premium loader improvements and debug messages
- Player bundle caching: cache check before patron status check
- Patreon token invalidation fix
- Patreon re-authentication prompt
- Patreon connection window showing connected without valid session token

## [1.16.0]

### Added
- **Controls settings** (General tab) with two new options:
  - **Hide Quick Controls** — hides the floating quick controls toolbar; on tablets also hides the settings button, on phones the settings button remains since Foundry's sidebar is hidden
  - **Hide Avatar Carousel** — hides the character avatar carousel; sheets can still be opened by double-tapping tokens
  - When quick controls are visible, Foundry's `#players` list is hidden on desktop to avoid overlap
  - Controls fieldset visible on desktop too with a note that settings apply to touch devices only

### Fixed
- `/stream` view no longer modified by Swipe VTT — Foundry's native stream view works as intended

### Removed
- Stream mode initialization (streamReady hook, background override, stream CSS, /stream redirect logic)

## [1.15.0]

### Added
- Player premium: cache-first fallback, version-based cache invalidation
- PF2e spellbook search

### Fixed
- Image optimizer button fixes

## [1.14.0]

### Added
- PF2e spellbook: signature spells, spontaneous casting, variable actions, rank fixes
- Collapsible card content in chat, chat drawer sizing improvements
- Memory diagnostics improvements
- Tools filter for standalone

### Fixed
- Tool rolls and standalone prepared data
- Reload loop fix

## [1.13.0]

### Fixed
- Scope mobile CSS rules to `body.swipe-vtt` to prevent desktop leakage
- GM-offline warnings: track user active state, fix notification visibility
- Roll dialog mode info font sizes

## [1.12.2]

### Added
- GM-offline warnings for standalone rolls, edits, and actions

### Fixed
- Chat toggle button z-index above chat drawer
- Settings checkbox color

## [1.12.1]

### Added
- Pinch-to-zoom for application windows with header touch handling
- Journal quick control, dynamic z-index for drawers
- Blade Runner chat styling

### Changed
- Clarify image optimizer descriptions to reassure desktop scenes are unaffected

## [1.12.0]

### Added
- PF2e NPC sheet: shield, initiative, traits, notes; hide feats/crafting
- PF2e inventory: native coin API, editable qty for contained items
- PF2e sheet: crafting, effects, feats, inventory, spellbook sections + roll dialog setting
- Gate mobile sheets on `enableMobileSheets` setting with fallback carousel

### Changed
- Sheet-only mode stays on `/game` with noCanvas instead of redirecting to `/stream`
- Gate standalone mode to supported systems only (dnd5e)

### Fixed
- Window header tap and position jump on mobile
- Temp Max row hidden in HP dialog for systems without tempmax (PF2e)
- Image optimizer dialog not showing scene analysis on first open

## [1.10.1]

### Added
- **Generic MobileTemplatePlacer** for all systems (PF2e, Daggerheart, etc.)
  - Template previews from any system are now touch-draggable on mobile
  - Uses PIXI childAdded detection on canvas.templates.preview
  - Initial position centers on user's token or viewport center
  - Proper system cleanup via synthetic rightdown to terminate system placement flows
- Generic system CSS overrides for PF2e actor sheets on mobile

### Fixed
- Mobile application dialog min-width and max-width sizing
- Settings user names truncation using max-width instead of white-space

## [1.10.0]

### Added
- **Standalone mode** for memory-constrained phones (iPhones, low-RAM Android)
  - Lightweight HTML app that bypasses Foundry's client entirely
  - Socket.io connection with session auth and real-time world data sync
  - Full character sheet rendering (combat, inventory, spellbook, features, biography, effects)
  - GM-proxied dice rolling with mobile roll dialog
  - Chat drawer with GM-relayed rendered HTML messages
  - Effects/conditions with status toggling
  - Hit die rolls, short rest, and long rest
  - Group actor Members tab with member summaries
  - Activity use, attack, and damage buttons
  - Premium bundle loading
  - Pause/unpause game and log out
- **Performance mode overlay dialog** for mobile devices
  - Native overlay replaces ApplicationV2 window on phones
  - Standalone as a selectable performance mode tier
  - Player-side mode override with reset button
  - Seamless navigation between standalone ↔ Foundry modes
- Invite URL override setting for VPN/proxy QR code URLs
- Stream view: compendium packs init, sheet config, GM journal sharing

### Fixed
- Species/background showing as raw IDs instead of names
- Item uses display when `value` is null (compute from `max - spent`)
- Activity damage formulas showing `@mod`/`@prof` instead of resolved values
- Save DC not displayed on save-type activities
- Token double-tap for unsupported actor types now opens native sheet
- Chat drawer crash in stream view
- Quick controls showing canvas buttons where no canvas exists
- enrichHTML crashes in standalone mode (try/catch across all sections)

### Changed
- Normalize item/class/feature images to 2.35rem across all systems
- Font variable fallback chain with `--mobile-font-fallback`
- Roll dialog scrollable body with max-height constraint
- Journal sheets fullscreen on mobile
- Rename "Connect Phone" to "Swipe QR Code"
- Deduplicate dice tooltip color/filter rules

## [1.7.4]

### Changed
- Sheet-Only mode now uses Foundry's stream view to reduce module load on iOS

## [1.7.1]

### Added
- Memory diagnostics utility for troubleshooting device performance

## [1.7.0]

### Added
- GM-side user mobile configuration
  - GM can set performance mode per-user from desktop settings
  - Force mode option for users whose devices won't load in default mode
  - Useful for iPhones with strict memory limits on heavy worlds

## [1.6.3]

### Changed
- Disable crlngn-ui floating dock on mobile devices
- Move video button between logout and volume in quick controls

## [1.6.1]

### Added
- Push-to-Talk button above quick controls toggle (touch-hold to broadcast)
- A/V settings button in camera dialog to open Foundry's config

## [1.6.0]

### Added
- Settings cleanup utility for orphaned module settings
- Workaround for Seasons & Stars infinite recursion crash on mobile

### Changed
- Allow GM to load premium via world token on new devices

## [1.5.0]

### Added
- Mobile camera dock enhancements
  - Floating, touch-draggable camera dock on phones (position: fixed, drag to reposition)
  - Camera quick controls dialog with Show/Hide Dock, Hide/Show All, and Speaker Only buttons
  - Speaker-only camera mode: CSS grid stacking with opacity crossfade, GM camera always visible as fallback
  - Speaker-only setting in Swipe VTT Settings under new Camera Views fieldset
  - Navigation arrows in camera controls to browse between camera views
  - Touch-hover simulation for camera view controls (tap to show, tap outside to dismiss)
  - Camera dock starts minimized on mobile devices
  - Camera dock hidden until module finishes applying layout classes
- CameraPopout touch drag support (Foundry popouts use mouse-only drag by default)
- Compatibility with crlngn-ui floating dock (skips conflicting handlers when active)

## [1.4.0]

### Added
- Opened module to all members of Patreon, even free. Rename Premium features to Amethyst Club features

### Fixed
- CSS breakpoints for hiding mobile controls

## [1.3.7]

### Added
- Party Group setting: GM can select a dnd5e Group actor as the party
  - Group members appear in the mobile carousel for all players with LIMITED+ permission
  - Works even without tokens on the current scene
- Group actor mobile sheet with 3 tabs (all free):
  - Members: shows avatar, name, class, AC, HP bar; tap to switch to that character
  - Inventory: editable currency grid, collapsible item categories, containers with contents, use button for consumables, expandable item details
  - Biography: enriched summary and full description
- Wake lock to prevent screen dimming and frequent reloads on mobile
- Improved display of Foundry game settings on mobile screen sizes

## [1.3.5]

### Added
- Quantity editor dialog for inventory items (tap quantity to adjust)
- Safari notification for iOS users about potential compatibility

### Changed
- Assistant GM can now load Amethyst Club features without needing to re-authenticate

## [1.3.2]

### Added
- Connect Phone: QR code dialog for connecting a phone as the same user
  - Scan QR code or copy link to bypass the join screen's greyed-out user restriction
  - Standalone phone-join page with auto-join flow and password prompt
  - "Connect Phone" button injected into User Configuration dialog
  - Auto-shows on desktop load with "Don't show again" user flag
  - Localhost detection uses LAN IP for QR code URL

### Fixed
- Minor refinements to canvas pan handling and hook cleanup

## [1.3.0]

### Added
- Expanded Sheet mode for tablets in canvas-disabled mode (premium)
  - Multi-column layout with 2-5 visible sections based on screen width
  - Responsive column sizing with min/max constraints
- Canvas-disabled background image with vignette overlay
  - Default castle background included, customizable via settings
  - File picker with Browse/Clear in settings
- Sidebar long-press handler for tablets (right-click equivalent)
  - Long-press on sidebar tab buttons triggers pop-out window
- Canvas pan detection: unfreezes canvas when external modules pan the viewport
- Dice So Nice prompt in Aggressive performance mode (optional, no longer automatic)

### Changed
- Desktop mobile mode setting renamed for clarity (`enabledOnDesktop`)
- Performance mode dialog: "Use 1x Resolution" renamed to "Disable Pixel Ratio Resolution"
- Aggressive mode description clarifies Dice So Nice is offered, not forced
- Mobile UI controls now visible in canvas-disabled mode on tablets
- Ability card styling refinements (font sizes, spacing, touch targets)
- Combat section: larger subtab touch targets, normalized font weights
- Condition items: larger min-height, improved active/inactive text colors
- Image popout max-height increased to 95dvh

### Fixed
- Character carousel now works without canvas (reads scene tokens directly)
- Canvas freeze indicator responding to external pan events
- Sheet button focus outline removed on mobile

## [1.2.8]

### Fixed
- Access for Assistant GM now follows the logic of player

## [1.2.7]

### Added
- iOS Automated Animations prompt now shows after Performance Mode selection

### Changed
- Reload prompt now triggers for all performance tab setting changes

### Fixed
- Effects tab condition buttons not visually updating after toggle

## [1.2.6]

### Added
- Safari iOS detection and automatic Dice So Nice optimization
  - Auto-sets DSN to low quality mode for WebGL compatibility
- Collapsible category headers in Combat tab (Weapons, Features, spell levels)
- Item descriptions in Combat tab (shown when item is expanded)
- Item properties in Combat tab (weapon properties, spell school/range/duration, etc.)
- Tap uses count to edit item/spell uses (all tabs)
- Touch-to-mouse adapter for external modules that only support mouse events
- Support for Carolingian Combat Tracker (#combat-popout visibility)

### Fixed
- Performance mode refactored: individual settings are now source of truth
- Canvas freeze indicator not appearing (initialization timing issue)

## [1.2.5] - 2026-01-21

### Added
- Warning when enabling Swipe VTT on desktop

### Changed
- Performance settings can now be saved independently of performance mode
- Image optimizer dialog clarifies that videos are not optimized

### Fixed
- Oversized image in Effects tab of D&D 5e sheet

## [1.2.4] - 2026-01-19

### Added
- Performance Mode dialog with device-based recommendations
- Weighted device tier detection (70% memory, 30% GPU)
- Shortcut to disable canvas entirely
- User overrides for Dice So Nice and Automated Animations
- Reload prompt after changing performance mode
- Container loots in dnd5e sheets

### Changed
- Canvas freeze is now free
- Image optimization is now free
- Fixed Disable Automated Animations / Dice So Nice settings 
- Hide "Enable Mobile Mode on Desktop" setting on mobile to avoid confusion
- Removed duplicate files


## [1.1.0] - 2026-01-16

### Added
- PIXI.Assets aliasing for optimized images on mobile
  - Optimized images now load directly instead of swapping after original loads
  - Prevents large images from being downloaded on mobile devices
- Registry validation on startup (GM only)
  - Removes stale entries for optimized files that no longer exist

## [1.0.16] - 2026-01-15

### Added
- World token system for offline GM premium access
  - Players can access Amethyst Club features when GM is offline using cached world tokens
  - World-scoped cache prevents cross-world cache leakage
  - 7-day token validity with automatic refresh
- Link code authentication for Patreon (alternative to popup auth)
  - 2-minute expiry for security
  - Previous codes invalidated when new one is generated
- Large image notification for GMs
  - Permanent warning when navigating to scenes with unoptimized images
  - Directs GM to Image Optimizer in settings

### Changed
- Removed skip functionality from Image Optimizer dialog
- Improved Premium Auth dialog to work correctly in DEV_MODE
- Localized "Sheet & Chat" fieldset legend

### Fixed
- Duplicate notification prevention for large image warnings
- Race condition in premium bundle loading vs canvasReady hook

## [1.0.8] - 2026-01-14

### Added
- Daggerheart adversary mobile sheet support
  - Adversary-specific header with HP/Stress display
  - Difficulty and Attack modifier stats display
  - Attack section using system.attack ActionField
  - Reaction roll button
  - Damage thresholds row (Minor/Major/Severe)
- Dynamic tab rendering based on actor type
  - PCs show 6 tabs: Traits, Loadout, Inventory, Features, Effects, Bio
  - Adversaries show 3 tabs: Traits, Features, Effects

### Fixed
- Tab navigation now properly updates when switching between actor types in carousel
- Adversary attacks now correctly use system.attack instead of weapon items
- Range labels properly localized using CONFIG.DH.GENERAL.range

## [1.0.7] - 2026-01-13

### Added
- Modular sheet architecture with base classes
- System router for multi-system support
- D&D 5e sections moved to dedicated directory
- Daggerheart system support (initial)

### Changed
- Refactored sheet architecture for better extensibility
- Dev mode support with production safety checks

## [1.0.3] - Previous

### Added
- Initial modular sheet architecture
- Base classes for drawer and sections

## [1.0.0] - Initial Release

### Added
- Mobile-friendly interface for Foundry VTT
- Touch controls and gesture recognition
- Mobile-optimized character sheets
- Pinch-zoom and pan gestures on canvas
- Token interaction via touch (tap, double-tap, long-press)
- Bottom drawer UI with avatar carousel
- D&D 5e character sheet support
- Amethyst Club features system with Patreon integration
- Socketlib integration for GM-player bundle sharing
