# Using headless Chrome as an automated screenshot tool
References:
- [Medium Post](https://medium.com/@dschnr/using-headless-chrome-as-an-automated-screenshot-tool-4b07dffba79a)
- [Google Dev Post](https://developers.google.com/web/updates/2017/04/headless-chrome)
- [Light House](https://developers.google.com/web/tools/lighthouse/)

## Install Vagrant Box
```
if ! type "brew" > /dev/null; then
  ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)";
fi
brew tap phinze/homebrew-cask && brew install brew-cask;
brew cask install vagrant;
brew cask install virtualbox;
```

## Initialize Vagrant Box
```
vagrant init ubuntu/trusty64; vagrant up --provider virtualbox
vagrant ssh
```

# On Vagrant Box
```
cd /vagrant
```

## Install Chrome ()
```
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb https://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
sudo apt-get update
sudo apt-get install -y google-chrome-stable
```

## Install Node
```
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install -y nodejs
```
## Install dependencies
```
npm init
npm install --save chrome-remote-interface minimist
```

# Run Chrome as background process
```
# https://chromium.googlesource.com/chromium/src/+/lkgr/headless/README.md
# --disable-gpu currently required, see link above
google-chrome --headless --hide-scrollbars --remote-debugging-port=9222 --disable-gpu &
```

# Take the screenshot
```
nodejs index.js --url="http://www.eff.org"
```
