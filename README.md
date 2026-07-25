# Linux-HELPGUI
this is a helpgui for linux steps: do "sudo apt install nano" if you dont have the libary then make a new file in  /usr/local/bin/ then name it helpgui and put in this code
 #!/usr/bin/env python3
import curses
import sys

pages = {
    "Python Basics": """Python Basics

Run a script:
  python3 file.py

Check version:
  python3 --version

Install packages:
  pip install <package>

Interactive shell:
  python3
""",

    "Python Advanced": """Python Advanced

Virtual environments:
  python3 -m venv env
  source env/bin/activate

Install from requirements:
  pip install -r requirements.txt

Run module:
  python3 -m <module>
""",

    "Sudo": """Sudo Commands

Run as root:
  sudo <command>

Repeat last command:
  sudo !!

Edit system files:
  sudo nano /etc/hosts
""",

    "APT Package Manager": """APT Package Manager

Update:
  sudo apt update

Upgrade:
  sudo apt upgrade
  sudo apt full-upgrade

Install:
  sudo apt install <package>

Remove:
  sudo apt remove <package>
  sudo apt purge <package>

List:
  apt list
  apt list --installed
  apt list --upgradable

Search:
  apt search <name>

Show info:
  apt show <package>

Fix broken:
  sudo apt --fix-broken install

Cleanup:
  sudo apt autoremove
  sudo apt clean
  sudo apt autoclean
""",

    "WSL Commands": """WSL Commands

Shutdown:
  wsl --shutdown

List distros:
  wsl -l -v

Set version:
  wsl --set-version Ubuntu 2

Install distro:
  wsl --install -d Ubuntu
""",

    "Networking": """Networking Commands

Show IP:
  ip a

Ping:
  ping google.com

DNS lookup:
  dig <domain>
  nslookup <domain>

Check ports:
  ss -tulnp
""",

    "Git": """Git Commands

Clone:
  git clone <url>

Commit:
  git add .
  git commit -m "message"

Push:
  git push

Branches:
  git branch
  git checkout <branch>
""",

    "Fastfetch": """Fastfetch Tips

Run:
  fastfetch

Config file:
  ~/.config/fastfetch/config.jsonc

Examples:
  fastfetch --logo arch_small
  fastfetch --structure cpu gpu os shell wm
"""
}

menu = list(pages.keys()) + ["Quit"]

def show_page(stdscr, title):
    stdscr.clear()
    curses.init_pair(2, curses.COLOR_YELLOW, curses.COLOR_BLACK)
    stdscr.addstr(0, 2, title, curses.color_pair(2) | curses.A_BOLD)

    lines = pages[title].split("\n")
    for i, line in enumerate(lines):
        stdscr.addstr(2 + i, 2, line)

    stdscr.addstr(22, 2, "Press any key to go back", curses.A_DIM)
    stdscr.getch()

def main(stdscr):
    curses.curs_set(0)
    curses.start_color()
    curses.init_pair(1, curses.COLOR_CYAN, curses.COLOR_BLACK)

    current = 0

    while True:
        stdscr.clear()
        stdscr.addstr(0, 2, "Filip's HelpGUI", curses.color_pair(1) | curses.A_BOLD)

        for i, item in enumerate(menu):
            if i == current:
                stdscr.addstr(i + 2, 2, "> " + item, curses.A_REVERSE)
            else:
                stdscr.addstr(i + 2, 2, "  " + item)

        stdscr.addstr(len(menu) + 3, 2, "Use ↑ ↓ to move, Enter to select", curses.A_DIM)

        key = stdscr.getch()

        if key == curses.KEY_UP and current > 0:
            current -= 1
        elif key == curses.KEY_DOWN and current < len(menu) - 1:
            current += 1
        elif key == 10:
            if menu[current] == "Quit":
                sys.exit(0)
            else:
                show_page(stdscr, menu[current])

curses.wrapper(main)









then save it and use the up and down arrow keys 
