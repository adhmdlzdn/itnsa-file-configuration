<a href="https://github.com/adrhmdlz/itnsa-lks-kotang" target="_blank"><img alt="GitHub hits" src="https://img.shields.io/github/last-commit/adrhmdlz/itnsa-lks-kotang?label=repository%20updated&style=flat-square"></a>

<h1 align="center">
  <!--
  <a href="http://www.amitmerchant.com/electron-markdownify"><img src="https://raw.githubusercontent.com/amitmerchant1990/electron-markdownify/master/app/img/markdownify.png" alt="Markdownify" width="200"></a>
  -->
  <br>
  ITNSA LKS Kota Tangerang 2023<br>
</h1>

<h4 align="center">Pembahasan terkait soal LKS (Lomba Kompetensi Siswa) SMK Kota Tangerang tahun 2023 bidang ITNSA (IT Network Systems Administration) untuk modul Client Server Environments. Diupdate secara bertahap sampai selesai.</h4>

<br>

## Materials
* GNU/Linux Debian 11
* Windows Server 2019
* Oracle VM VirtualBox

<br>

## Topology
<img src="https://raw.githubusercontent.com/adrhmdlz/itnsa-lks-kotang/master/assets/topology.png">

<br>

## Configuration That I Use

* A-CLT :
	- eth0 (enp0s3) = 192.168.10.10 (static)

* A-RTR :
	- eth0 (enp0s3) = 192.168.10.1 (static)
	- eth1 (enp0s8) = - 172.16.10.1 (static)
			- 10.10.10.1 (VPN)
	- eth2 (enp0s9) = bridge adapter (DHCP)

* B-RTR :
	- eth0 (enp0s3) = - 172.16.10.2 (static)
			- 10.10.10.2 (VPN)
	- eth1 (enp0s8) = DHCP IP from B-SRV
	- eth2 (enp0s9) = bridge adapter (DHCP)

* B-SRV :
	- ethernet = same adapter like eth1 B-RTR

<br>

## Task

* Basic Configuration
	- For all machines in the given topology, do the following :
	  - OS installed
	  - Hostname configured
	  - IP address set
	  - Timezone set to Asia/Jakarta

* Client Addressing
	- Make sure clients in the internal network A (A-CLT) can automatically lease address from A-RTR (DHCP)
	- Make the leased address for A-CLT stay by mapping its hardware (Static)

* Intersite Connection
	- Configure OpenVPN for A-RTR and B-RTR to established site-to-site VPN.

* Directory Service
	- Set B-SRV as the Primary Domain Controller of beta.net forest
	- Create User0001-User1000

* DNS
	- A-CLT can access soup and drive dns but not the primary dns from B-SRV
	- DNS servers should be secured via IP whitelisting and cyrptography

* Web
  - Configure two website :
	- drive.beta.net :
		- Only User0500-User0699 can access this site.
		- should show the directory listing of C:\www\root\drive.beta.net in B-SRV
		- Proxied by B-RTR using HAProxy
	- soup.beta.net :
		- Hosted in A-RTR using Nginx
		- Only Accessible from A-CLT
		- Webroot is located in /srv/www/soup.beta.net

* Storage
	- Share the path /srv/www/soup.beta.net using NFSv4
	- NFS share should only be accessible via A-CLT. Use a level 10 RAID as the underlying block storage

* File Sharing
	- Share the C:\share\collaboration directory in B-SRV via SMB. Allow only .html and .txt files whose size is no bigger than 5 MB
	- Limit access to User0300-User0499

* Backup
	- Configure a scheduler using SystemD in A-RTR to backup the content of soup.beta.net to B-RTR in C:\share\collaboration\soup.beta.net
	- The backup should happen every hour



<!--
<p align="center">
  <a href="https://badge.fury.io/js/electron-markdownify">
    <img src="https://badge.fury.io/js/electron-markdownify.svg"
         alt="Gitter">
  </a>
  <a href="https://gitter.im/amitmerchant1990/electron-markdownify"><img src="https://badges.gitter.im/amitmerchant1990/electron-markdownify.svg"></a>
  <a href="https://saythanks.io/to/bullredeyes@gmail.com">
      <img src="https://img.shields.io/badge/SayThanks.io-%E2%98%BC-1EAEDB.svg">
  </a>
  <a href="https://www.paypal.me/AmitMerchant">
    <img src="https://img.shields.io/badge/$-donate-ff69b4.svg?maxAge=2592000&amp;style=flat">
  </a>
</p>



<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#how-to-use">How To Use</a> •
  <a href="#download">Download</a> •
  <a href="#credits">Credits</a> •
  <a href="#related">Related</a> •
  <a href="#license">License</a>
</p>


[//]: ![screenshot](https://raw.githubusercontent.com/amitmerchant1990/electron-markdownify/master/app/img/markdownify.gif)
[//]: # (screenshot terhadap program yang dibuat)


## Key Features

* LivePreview - Make changes, See changes
  - Instantly see what your Markdown documents look like in HTML as you create them.
* Sync Scrolling
  - While you type, LivePreview will automatically scroll to the current location you're editing.
* GitHub Flavored Markdown  
* Syntax highlighting
* [KaTeX](https://khan.github.io/KaTeX/) Support
* Dark/Light mode
* Toolbar for basic Markdown formatting
* Supports multiple cursors
* Save the Markdown preview as PDF
* Emoji support in preview :tada:
* App will keep alive in tray for quick usage
* Full screen mode
  - Write distraction free.
* Cross platform
  - Windows, macOS and Linux ready.

## How To Use

To clone and run this application, you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer. From your command line:

```bash
# Clone this repository
$ git clone https://github.com/amitmerchant1990/electron-markdownify

# Go into the repository
$ cd electron-markdownify

# Install dependencies
$ npm install

# Run the app
$ npm start
```

> **Note**
> If you're using Linux Bash for Windows, [see this guide](https://www.howtogeek.com/261575/how-to-run-graphical-linux-desktop-applications-from-windows-10s-bash-shell/) or use `node` from the command prompt.


## Download

You can [download](https://github.com/amitmerchant1990/electron-markdownify/releases/tag/v1.2.0) the latest installable version of Markdownify for Windows, macOS and Linux.

## Emailware

Markdownify is an [emailware](https://en.wiktionary.org/wiki/emailware). Meaning, if you liked using this app or it has helped you in any way, I'd like you send me an email at <bullredeyes@gmail.com> about anything you'd want to say about this software. I'd really appreciate it!

## Credits

This software uses the following open source packages:

- [Electron](http://electron.atom.io/)
- [Node.js](https://nodejs.org/)
- [Marked - a markdown parser](https://github.com/chjj/marked)
- [showdown](http://showdownjs.github.io/showdown/)
- [CodeMirror](http://codemirror.net/)
- Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)
- [highlight.js](https://highlightjs.org/)

## Related

[markdownify-web](https://github.com/amitmerchant1990/markdownify-web) - Web version of Markdownify

## Support

<a href="https://www.buymeacoffee.com/5Zn8Xh3l9" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/purple_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

<p>Or</p> 

<a href="https://www.patreon.com/amitmerchant">
	<img src="https://c5.patreon.com/external/logo/become_a_patron_button@2x.png" width="160">
</a>

-->

<br>

## You Might Be Interest

- [Km Gpp](https://github.com/adrhmdlz/km-gpp) - A simple program using Python language
- [Simptech.id](https://github.com/adrhmdlz/simptech-id) - A simple website using only HTML, CSS and JS

---

> [adrhmdlz.github.io](https://adrhmdlz.github.io) &nbsp;&middot;&nbsp;
> Gmail [@adrianalzidan35](mailto:adrianalzidan35@gmail.com) &nbsp;&middot;&nbsp;
> GitHub [@adrhmdlz](https://github.com/adrhmdlz) &nbsp;&middot;&nbsp;
> Instagram [@adrhmdlz](https://instagram.com/adrhmdlz) &nbsp;&middot;&nbsp;
> LinkedIn [@adrhmdlz](https://www.linkedin.com/in/adrhmdlz/)



