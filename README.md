# Electron PWA Wrapper

A sample wrapper app to package your Progressive Web App into a Desktop Application using [Electron](https://github.com/electron/electron).

Drafted for the future Desktop-version of my [Leasing Calculator](https://www.leasingrechnen.at) Web App using [React](https://github.com/facebook/react), [Redux](https://github.com/reactjs/redux), [Materialize.css](https://github.com/Dogfalo/materialize) and a lot of Offline-First love over at [leasingrechnen.at](https://www.leasingrechnen.at).

### Early development stage, please don't use for your projects yet.

## Features
- loading animation window for first boot
- handle connectivity issues natively in the wrapper
- build with electron-builder

## Upcoming Features
- macOS TouchBar support
- macOS custom TitleBar

## Wanna give it a try?
- clone repository, *cd* into the directory
- run `npm install` to get the dependencies
- run `npm run electron` to start the app
- check out */app/constants.js* for some options (e.g. setting your own URL)

## Customizing
- Place your Tray- and App-Icons into `src/assets`.
- Change `app/app_menu_template.js` to use your own Menu Items.
- Check `app/constants.js` for localizing your Strings (this project is German by default).
	- if you know how to do multi-language in Electron, a Pull-Request would be much appreciated!!
- While in `app/constants.js`, check the `settings` and `mainWindow` sections too.
- The Offline- and Loading-Screens are located in `src/offline.html` and `src/loader.html`, their corresponding images and styles in `src/res`.

## Building with [electron-builder](https://github.com/electron-userland/electron-builder)
Electron-PWA-Wrapper comes with *electron-builder* preconfigured for macOS (dmg, mas) and Windows (Appx + Portable).

### Preperations
- You'll need to 
	- look up your `package.json` and put in your App's values in the *build* section
	- and put all the required graphics into the `build` directory.
	- See the below, and the [electron-builder Docs](https://www.electron.build) for further details!
- run `npm run build` or `./node_modules/.bin/electron-builder build` to start the build. Your app files will be located in the `dist` folder.

### Build for macOS App Store
- Have a machine running the latest macOS ready, and latest _XCode_ installed.
- Get a paid Apple Developer membership (~€99,- per year) and create Certificates, Identifiers and Provisioning Profiles for macOS:
	- Certificates: Production -> _Mac App Distribution_ and _Mac Installer Distribution_.
	- Identifiers: App IDs -> create one with your package/bundle name (e.g. 'com.example.myawesomeapp').
	- Provisioning Profiles: Distribution -> _Mac Distribution_ for the Identifier you just created.
- Download the certificates and double-click them to get them installed in your local Keychain.
- Download and copy your Provisioning Profile to the project root and rename it to `embedded.provisionprofile`.
- Make sure you've updated your `package.json`->`build`-> _appId_, _productName_, _copyright_ and _mac_->_category_
- Put the required icons in place:
	- in `build`->_icon.iconset_, replace all the icons in the folder. Sizes and namings are important!
	- open the terminal, navigate to `build` and run the following command to create your `icon.icns` from the iconset you've just populated.
		- `iconutil -c icns icon.iconset`
- Edit the `build/Info.plist` and `build/entitlements.mas.plist` and replace _YourTeamId_ and _YourPackageId_.
	- You can find your Team ID on the Apple Developer Account in _Membership_.
	- Your package ID is the bundle identifier you've created in step 1.
- Run `npm run build` from the terminal.
	- If it fails, you might have to give the process proper permission by running `sudo ./node_modules/.bin/electron-builder build` instead.

### Build for Windows Store
- Have a machine running Windows 10 Enterprise ready, with all latest updates and `windows-build-tools` installed.
- Get a paid [Windows Dev Center Publisher Account](https://developer.microsoft.com/en-us/store/register) (~€25,- once) and sign up for [DesktopBridge](https://developer.microsoft.com/en-us/windows/projects/campaigns/desktop-bridge) Support for your app.
- Create your App in the [Windows Dev Dasboard](https://developer.microsoft.com/en-us/dashboard/windows/overview) to get the values for the next step.
- Update your `package.json`->`build`->`win`-> _legalTrademarks_ and _publisherName_, and all the attributes in `build`->`appx`.
- Put the required icons in place:
	- in `build`: _icon.ico_
	- in `build/appx`: replace all the icons in the folder. Sizes and namings are important!
- Run `npm run build` from the command line (preferably from PowerShell).


## License
[GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html) - if you use it, we wanna see it!
