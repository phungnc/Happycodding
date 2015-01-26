## Install Node.js (For Windows)

(I'm not try yet)
1. Install [nodist](https://github.com/marcelklehr/nodist)
2. Use nodist to install node.js version that you like

## Install Node.js (For Mac)

### Install nvm

	git clone git://github.com/creationix/nvm.git ~/.nvm
	source ~/.nvm/nvm.sh

### Install node.js via nvm

Node version list

	nvm ls-remote
	v0.11.11
    v0.11.12
    v0.11.13
    v0.11.14

Install latest version

    nvm install 0.11.14

Confirm

    node -v

Finish!

### nvm setting

Set default node.js version

	nvm alias default v0.11.14

Edit ~/.bash_profile

	vi ~/.bash_profile

In .bash_profile file add:

	if [[ -s ~/.nvm/nvm.sh ]];
 		then source ~/.nvm/nvm.sh
	fi
