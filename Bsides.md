# For dummies
notes for things will be on youtube/ somehwere on internet later

communities 
- capture the flag
	- cryptography steganography
	- application security
	- OSINT
	- reverse enginerring
	- trivia
- the keep
	- video game where boss fights are you running exploits
	- good for beginners apparently 
- saintcon
	- another thing like bsides but in october, is larger apparently

abcdefghijklmnopqrstuvwxyz

# Desktop applications 
What is a desktop appilication
- compiles and runs on windows/mac/etc
- executes by a local user
- may include UI andCLI 

Threat modeling
	identifify all components and features directly accessible to an attacker
	user roles/ threat actors: security relevant privileges an attacker can assume
	critical assets; essential components of the system, dependend on business risks
	attacker goes: what an attacker wants out of each asset
- attck surface
- files libraries, drivers, internal communications, backedn ommunication
- user roles adn threat actors: athutehnicated users, local attaackers, network attackers
- critical assets: confidential information, hardware resources

Recon
- application enumeration
- Dynamic testing
	- assessing the application while it is running
	- key areas
		- network traffic analysis
			- evaluate open ports
			- inspect traffic
			- using proxies to monitor traffic
		- debugger analysis
			- help you see system calls
		- file system - local authN and authZ
			- local credential storage
			- see which files are being used, what is in th efiles
		- injection testing
		- memory analysis
- Static testing
	- assessing the applications code and binaries without execution
		- reverse engineering
			- if we dont have access to source code
				- some decompiler tools are available, with specific versions for different languages
		- source code review
			- you can find hard coded items in htere a lot of the time
			- 'nosey parker' apparently helps you find the hard coded things
			- insecure functions
				- unprotected stack, insecure deserialization, database injection, file manipulation etc

Exploit
- Injection testing
	- most important risk in 'mumbles'
	- usually depends on language it is written in, like SQL injections
	- people will type in special characters and see how the program responds to it
- Unquoted service path (windows)
	- idk what a service path is but if you have spaces in there an attacker can run a program in places where it shouldn't or something
- Library hijacking
	- replacing legit libraries with malicious ones
- IPC vulnerabilities
	- interproess communication describes any mechanism where data is shared between processes
	- if permissions are not configured properly data leaks happen or something malicious can be passes into the application
- MITM/AITM attacks
	- machine in the middle
	- attacker in the middle
	- requires the attacker to intercept or modify traffic on the wire
- Uninstall script vulnerability
	- can get you root access if you put a command like 'rm' in a temp directory, or stuff like that to open a new shell
	- basiclaly if you tell the computer where to look with relative paths you can do some cheesy stuff

# Evolution of auth



look up later
- federation
- API keys
- security keys
- SSO

authentication guideline NIST SP 800-63


eveolution
- passwords
- password hashing since all passwords would be stored somehwere like a txt file
- password complexity since people are predictable
- password managers
- identity federation
	- i think this is like being able to have the same user on multiple devices
- social login
	- like 'login with google'
	- you dont need separate accounts for everything, lets services depend on larger platforms for passwords and authenticatoin
- API keys
- secret managers
	- for API keys
- OAuth
	- short lived access tokens
- Multi factor authentication
	- having another form of verificaion other than just a password
- security keys
	- google did some study on its employees and this got rid of phishing attacks dont really know how it works though
- Passkeys

what should you do
- for a service
	- only SSO with WebAuthn - no passwords
	- Build OAuth scopes
- for an organization
	- MFA as soon as possible
	- OAuth use via your IdP