<div align="center">

<!-- HEADER — no vercel dependency -->
<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=900&size=45&duration=2000&pause=500&color=00FF41&center=true&vCenter=true&repeat=true&width=700&height=70&lines=%E2%9A%A1+CyberSoul404+%E2%9A%A1" alt="Header" />

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&duration=2500&pause=600&color=39FF14&center=true&vCenter=true&repeat=true&width=800&height=45&lines=root%40CyberSoul%3A~%24+sudo+whoami;%5B+CLASSIFIED+%5D+Blake+%2F+CyberSoul404;Breaking+Systems+to+Build+Better+Ones+%F0%9F%94%90;Powered+by+Kali+Linux+%26+Caffeine+%E2%98%95;%3E+All+your+base+are+belong+to+us;%3E+Access+Granted.+Welcome%2C+Hacker." alt="Typing SVG" />

<br/>

<!-- STATUS BADGES — shields.io always works -->
<img src="https://img.shields.io/badge/STATUS-ACTIVE-00ff41?style=for-the-badge&labelColor=0d1117&logo=circle&logoColor=00ff41" />
<img src="https://img.shields.io/badge/OS-Kali_Linux-557C94?style=for-the-badge&labelColor=0d1117&logo=kalilinux&logoColor=557C94" />
<img src="https://img.shields.io/badge/FOCUS-Ethical_Hacking-ff6b35?style=for-the-badge&labelColor=0d1117" />
<img src="https://komarev.com/ghpvc/?username=CyberSoul404&label=VISITORS&color=00ff41&style=for-the-badge&labelColor=0d1117" />

</div>

---

## <img src="https://media.giphy.com/media/WUlplcMpOCEmTGBtBW/giphy.gif" width="40"> `$ whoami`

<img align="right" alt="Hacking GIF" src="https://media.giphy.com/media/RbDKaczqWovIugyJmW/giphy.gif" width="380" />


  def philosophy(self):
        return {
            "offensive": "Think like an attacker",
            "defensive": "Build like a fortress",
            "mindset":   "Break it to make it better"
        }

me = CyberSoul()
print(me.passion)  # → Hack ethically. Protect fiercely.

<br clear="right"/>
<div align="center">
⚡ Tech Arsenal
<!-- SKILLS — shields.io badges, 100% reliable -->
🔤 Languages
PythonBashCJavaScriptHTML5CSS3

🔐 Security Tools
WiresharkBurp SuiteMetasploitNmapHashcatJohnHydraAircrack-ng

🐧 OS & Infrastructure
Kali LinuxParrot OSUbuntuArchDockerVirtualBox

🐍 Python Stack
FlaskSeleniumScapyRequestsBeautifulSoupCryptography

🛠️ Dev Tools
GitGitHubVS CodeNeovimNginxMySQLPostgreSQL

</div>


🐍 Code Showcase
<details> <summary><b>🔍 Ethical Port Scanner</b></summary>
#!/usr/bin/env python3
"""
██████╗  ██████╗ ██████╗ ████████╗    ███████╗ ██████╗ █████╗ ███╗   ██╗
██╔══██╗██╔═══██╗██╔══██╗╚══██╔══╝    ██╔════╝██╔════╝██╔══██╗████╗  ██║
██████╔╝██║   ██║██████╔╝   ██║       ███████╗██║     ███████║██╔██╗ ██║
██╔═══╝ ██║   ██║██╔══██╗   ██║       ╚════██║██║     ██╔══██║██║╚██╗██║
██║     ╚██████╔╝██║  ██║   ██║       ███████║╚██████╗██║  ██║██║ ╚████║
╚═╝      ╚═════╝ ╚═╝  ╚═╝   ╚═╝       ╚══════╝ ╚═════╝╚═╝  ╚═╝╚═╝  ╚═══╝
  CyberSoul404 | Ethical Port Scanner v2.0 | Use responsibly.
"""
import socket
import concurrent.futures
from rich.console import Console
from rich.table import Table
from rich.progress import Progress, SpinnerColumn, BarColumn, TextColumn
from datetime import datetime

console = Console()

def probe_port(target: str, port: int, timeout: float = 0.5) -> dict | None:
    try:
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            s.settimeout(timeout)
            if s.connect_ex((target, port)) == 0:
                try:
                    banner = s.recv(1024).decode(errors="ignore").strip()
                except Exception:
                    banner = ""
                service = socket.getservbyport(port, "tcp") if port < 1024 else "unknown"
                return {"port": port, "service": service, "banner": banner[:60]}
    except Exception:
        return None

def stealth_scan(target: str, port_range: range, max_workers: int = 200) -> list:
    results = []
    table = Table(title=f"[bold green]🔍 Scan Results — {target}[/bold green]",
                  border_style="green", show_lines=True)
    table.add_column("Port", style="cyan bold", width=8)
    table.add_column("Service", style="yellow")
    table.add_column("Banner", style="dim white")

    with Progress(
        SpinnerColumn(spinner_name="dots12", style="green"),
        TextColumn("[bold green]Scanning {task.description}"),
        BarColumn(bar_width=40, complete_style="green"),
        TextColumn("[cyan]{task.completed}/{task.total}"),
        console=console
    ) as progress:
        task = progress.add_task(f"[{target}]", total=len(port_range))
        with concurrent.futures.ThreadPoolExecutor(max_workers=max_workers) as pool:
            futures = {pool.submit(probe_port, target, p): p for p in port_range}
            for future in concurrent.futures.as_completed(futures):
                progress.advance(task)
                result = future.result()
                if result:
                    results.append(result)
                    table.add_row(str(result["port"]),
                                  result["service"],
                                  result["banner"] or "—")

    console.print(table)
    console.print(f"\n[bold green]✓ Scan complete — {len(results)} open port(s) found[/bold green]")
    return sorted(results, key=lambda x: x["port"])

if __name__ == "__main__":
    stealth_scan("127.0.0.1", range(1, 10000), max_workers=500)
</details> <details> <summary><b>🌐 OSINT Username Recon Tool</b></summary>
#!/usr/bin/env python3
"""Multi-platform username recon — CyberSoul404"""
import asyncio, aiohttp
from rich.console import Console
from rich.table import Table

PLATFORMS = {
    "GitHub":    "https://github.com/{}",
    "Twitter":   "https://twitter.com/{}",
    "Instagram": "https://instagram.com/{}",
    "Reddit":    "https://reddit.com/user/{}",
    "HackerOne": "https://hackerone.com/{}",
    "TryHackMe": "https://tryhackme.com/p/{}",
}

async def check(session, platform, url, username):
    try:
        async with session.get(url.format(username), timeout=aiohttp.ClientTimeout(total=5)) as r:
            return platform, r.status == 200, url.format(username)
    except Exception:
        return platform, False, url.format(username)

async def recon(username: str):
    console = Console()
    table = Table(title=f"🔍 Recon: [green]{username}[/green]", border_style="green")
    table.add_column("Platform", style="cyan")
    table.add_column("Status")
    table.add_column("URL", style="dim")
    async with aiohttp.ClientSession() as session:
        tasks = [check(session, p, u, username) for p, u in PLATFORMS.items()]
        results = await asyncio.gather(*tasks)
    for platform, found, url in results:
        status = "[bold green]✓ FOUND[/bold green]" if found else "[red]✗ NOT FOUND[/red]"
        table.add_row(platform, status, url)
    console.print(table)

asyncio.run(recon("CyberSoul404"))

</details>
📊 System Monitor
<div align="center"> <!-- STATS — generated by GitHub Actions, stored in YOUR repo. Always loads. --> <a href="https://github.com/CyberSoul404"> <img src="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/profile-summary-card-output/chartreuse_dark/0-profile-details.svg" width="97%" alt="Profile Details" /> </a> <br/> <a href="https://github.com/CyberSoul404"> <img src="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/profile-summary-card-output/chartreuse_dark/1-repos-per-language.svg" width="48%" alt="Repos per Language" /> <img src="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/profile-summary-card-output/chartreuse_dark/2-most-commit-language.svg" width="48%" alt="Most Commit Language" /> </a> <br/> <a href="https://github.com/CyberSoul404"> <img src="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/profile-summary-card-output/chartreuse_dark/3-stats.svg" width="48%" alt="Stats" /> <img src="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/profile-summary-card-output/chartreuse_dark/4-productive-time.svg" width="48%" alt="Productive Time" /> </a>
<br/><br/>

<!-- STREAK — demolab.com confirmed working from India --> <a href="https://github.com/CyberSoul404"> <img src="https://streak-stats.demolab.com?user=CyberSoul404&theme=dark&hide_border=true&background=0d1117&ring=00ff41&fire=ff6b35&currStreakLabel=00ff41&sideLabels=00ff41&dates=888888&stroke=0d1117" height="180" alt="Streak Stats" /> </a> </div>
🐍 Contribution Snake
<div align="center"> <picture> <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/github-contribution-grid-snake-dark.svg" /> <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/github-contribution-grid-snake.svg" /> <img alt="Snake animation" src="https://raw.githubusercontent.com/CyberSoul404/CyberSoul404/output/github-contribution-grid-snake-dark.svg" width="100%" /> </picture> </div>
📡 Mission Status
<div align="center">
🎯 Objective	📊 Progress	🔖 Status
🔭 Build offensive cyber toolkit	█████████░ 92%	🟢 Active
🌱 Master advanced pentesting	████████░░ 78%	🟢 Active
🔍 OSINT & passive recon techniques	███████░░░ 68%	🟡 Learning
🐛 Reverse engineering & malware analysis	█████░░░░░ 48%	🟡 Learning
🏴 CTF competitions & writeups	████████░░ 80%	🟢 Active
📜 CEH / eJPT Certification	██████░░░░ 60%	🟡 In Progress
🤝 Open-source security contributions	█████░░░░░ 50%	⚪ Pending
</div>
🎯 Weekly Ops
<div align="center">
🗓️ Day	🔐 Mission	⚡ Status
MON	Code review + vulnerability hunting	✅
TUE	Build & test new security tools	✅
WED	CTF challenges + writeups	✅
THU	OSINT research + recon practice	🔄
FRI	Documentation + GitHub updates	⏳
SAT	Open-source contribution	⏳
SUN	Deep study: exploit dev / reversing	⏳
</div>
📬 Connect
<div align="center"> <a href="mailto:your-email@gmail.com"> <img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0d1117" /> </a> <a href="https://linkedin.com/in/yourprofile"> <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0d1117" /> </a> <a href="https://twitter.com/yourhandle"> <img src="https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white&labelColor=0d1117" /> </a> <a href="https://discord.com/users/yourid"> <img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white&labelColor=0d1117" /> </a> <a href="https://app.hackthebox.com/profile/yourprofile"> <img src="https://img.shields.io/badge/HackTheBox-9FEF00?style=for-the-badge&logo=hackthebox&logoColor=black&labelColor=0d1117" /> </a> <a href="https://tryhackme.com/p/yourprofile"> <img src="https://img.shields.io/badge/TryHackMe-212C42?style=for-the-badge&logo=tryhackme&logoColor=white&labelColor=0d1117" /> </a> </div>
<div align="center">
>>> print("The quieter you become, the more you can hear.")
>>> print("— Kali Linux motto")
<br/> <img src="https://img.shields.io/badge/Crafted_with_💚_by-CyberSoul404-00ff41?style=for-the-badge&labelColor=0d1117" />
<sub><i>Hack ethically. Build relentlessly.</i></sub>

</div> ```


```python

#!/usr/bin/env python3
# ╔══════════════════════════════════════════╗
# ║   CyberSoul404  |  Security Research    ║
# ║   Version: 4.0.4  |  Build: STABLE      ║
# ╚══════════════════════════════════════════╝

class CyberSoul(EthicalHacker):

    def __init__(self):
        self.alias      = "CyberSoul404"
        self.name       = "Blake"
        self.os         = "Kali Linux 🐧"
        self.editor     = "NeoVim / VSCode"
        self.languages  = ["Python", "Bash", "C", "JS"]
        self.tools      = ["Burp", "Nmap", "Wireshark",
                           "Metasploit", "John", "Hashcat"]
        self.learning   = ["Advanced Pentesting",
                           "OSINT", "Reverse Engineering",
                           "Exploit Development"]
        self.passion    = "Hack ethically. Protect fiercely."

  
    
