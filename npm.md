## How to install it with NVM (node version manager)
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
nvm install node
nvm use node
```
> Installing npm wihtout NVM is described in the Appendix.

## How to install package
```sh
npm i 					// alias for install
npm install				// install everything in package.json
npm install <package-name>		// install package
npm install --save <package-name>	// install package to the project
```

## How to uninstall package
```
npm uninstall <package-name>
```

## How to update 
```sh
npm update			// update production packages
npm update --dev 		// update dev packages
npm update -g 			// update global packages
npm update <package-name>	// update package
```

## `npx` vs `npm`
> `npx` runs package, `npm` install it

```sh
npx create-react-app <project-name>
```

## Appendix
### How to uninstall npm
```sh
sudo apt-get remove nodejs npm

sudo rm -rf /usr/local/bin/npm /usr/local/share/man/man1/node* /usr/local/lib/dtrace/node.d ~/.npm ~/.node-gyp /opt/local/bin/node /opt/local/include/node /opt/local/lib/node_modules 

sudo rm -rf /usr/local/lib/node*

sudo rm -rf /usr/local/include/node*

sudo rm -rf /usr/local/bin/node*

sudo rm -rf /usr/local/{lib/node{,/.npm,_modules},bin,share/man}/npm*
```
### How to install npm 
```sh
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install nodejs
```

> [Current NodeJS releases](https://nodejs.org/en/about/releases/)

### How to install packages without `sudo`
```sh
mkdir "${HOME}/.npm-packages"
npm config set prefix "${HOME}/.npm-packages"
```
> Add the following to your .bashrc/.zshrc:
```sh
NPM_PACKAGES="${HOME}/.npm-packages"

export PATH="$NPM_PACKAGES/bin:$PATH"

# Unset manpath so we can inherit from /etc/manpath via the `manpath` command
unset MANPATH # delete if you already modified MANPATH elsewhere in your config
export MANPATH="$NPM_PACKAGES/share/man:$(manpath)"
``` 


## Sources
[1]: [How to install globally without sudo](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md) 
[2]: [Node version manager](https://github.com/nvm-sh/nvm)
