# Session restore

Approved scope: automatically restore normal windows, tab order and custom
titles/colors, pane layout and split proportions, each pane's working directory,
the selected tab/pane, and window position/size on ordinary startup.

Persist a versioned session snapshot separately from configuration. Save changes
after a short delay, and flush before application teardown. Explicitly closed
tabs/windows disappear from the live session; quitting preserves the remaining
workspace. The final window close preserves its workspace for the next launch.
Use a temporary file and atomic replacement. Invalid snapshots must not prevent
startup. Missing directories fall back to home; windows on disconnected displays
must return to a visible display. Session restore is enabled by default with an
option to disable it. Explicit CLI commands/directories start independently.

Recreate shells, not running processes. Do not replay commands or persist terminal
output, SSH connections, editors, environment variables, or process memory.

Alternative considered: save only at clean exit. Rejected because crashes and
forced exits would lose layout changes. Reuse the existing layout tree rather than
adding a parallel split representation at runtime.

Validation: snapshot parsing/version/limits, file round trips and corruption,
layout serialization/restoration (including nested splits and proportions),
selection/tab metadata, directory fallback and window placement, and relevant
Rust checks. Native OS geometry and shell behavior need a GUI smoke test.
