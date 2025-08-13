# CODETECH-Task1
NAME : BALLA NEERAJ
Company : CODTECH IT SOLUTIONS
ID : CT08DH138
Domain: Data Analytics
Duration : june to August 2025
Mentor:  Neela Santosh Kumar

1. Purpose
Tracks important files or directories on a system and alerts if they are modified, deleted, or changed.

Uses cryptographic hash algorithms (MD5, SHA1, SHA256, SHA512, BLAKE2b) to detect changes.

Stores baseline hashes and change logs in an SQLite database.

Can be operated via:

GUI (Tkinter) – User-friendly interface for managing monitored files.

CLI (Command Line) – For automation, scripting, or server-side use.

2. Components in Code
A. FileIntegrityMonitor Class (Core monitoring engine)
Handles all backend logic:

Database Initialization
Creates two SQLite tables:

file_hashes – Stores file path, size, algorithm, hash value, timestamp, and status.

change_log – Records modifications, deletions, old/new hashes, and sizes.

Hash Calculation

Reads file in chunks and computes hash with chosen algorithm.

File/Directory Management

add_file_to_monitor() – Adds a single file.

add_directory_to_monitor() – Adds entire directories (recursive optional, with include/exclude patterns).

Integrity Checking

check_file_integrity() – Compares current hash with stored baseline; logs if changed or deleted.

check_all_monitored_files() – Batch check for all files.

Data Retrieval & Maintenance

get_monitored_files() – Retrieves all tracked files’ details.

get_change_history() – Fetches logged changes.

remove_from_monitoring() – Stops tracking a file.

update_baseline() – Updates stored hash after intentional change.

B. FileIntegrityGUI Class (Tkinter GUI frontend)
Provides graphical interface with four main tabs:

📁 Monitor Files Tab

Add files/directories to monitor.

Choose hash algorithm.

Enable/disable recursive folder monitoring.

View list of monitored files with size, hash, date added.

Right-click menu: Check Integrity, Update Baseline, Remove, Show Info.

🔍 Check Integrity Tab

Check all files or selected files.

Generate a human-readable report.

Enable auto-checking every X seconds.

📜 Change History Tab

Shows modified/deleted files.

Refresh and clear history buttons.

⚙️ Settings Tab

Database stats (number of monitored files, changes, algorithm breakdown).

Export monitored file list to JSON (for backup/sharing).

Import monitoring list from JSON file.

Extra GUI Features:

Progress dialog when scanning large directories.

Colored emojis & labels for user-friendly status display.

Pop-up alerts for detected changes.

C. Command Line Interface (CLI)
The tool can be run headless (without GUI) for automation:

bash
python monitor.py --cli --add-file /path/to/file --algorithm sha256
python monitor.py --cli --check /path/to/file
python monitor.py --cli --check-all
python monitor.py --cli --list
python monitor.py --cli --remove /path/to/file
CLI Options:

--add-file – Monitor a file.

--add-dir – Monitor directory.

--check – Check a single file.

--check-all – Check all monitored files.

--list – Show monitored files.

--remove – Remove from monitoring.

--recursive – Recursive folder monitoring.

--algorithm – Choose hash type.

--db – Custom SQLite database path.

3. How It Works (Flow)
Add Files/Dirs:
Calculates selected hash, stores path+hash+size in DB.

Check Integrity:
Reads file → Calculates hash → Compares with stored → Logs changes in change_log table.

Alerts & Logs:

GUI: popup messages, results tab.

CLI: prints results to terminal.

History & Reporting:
Shows all changes; can export to reports.

4. Use Cases
Security: Detecting unauthorized modification of system files.

Compliance: Assuring file integrity for audits.

Development: Tracking configuration file changes.

Forensics: Verifying evidence hasn’t been altered.

5. Key Strengths
✔ Supports multiple hash algorithms for flexibility.
✔ Offers both interactive GUI and automation-friendly CLI.
✔ Stores logs persistently in SQLite – keeps historical changes.
✔ Export/Import config – easy to migrate setup.
✔ Auto-check feature – continuous monitoring without user intervention.
