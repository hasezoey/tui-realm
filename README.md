# tui-realm

<p align="center">
  <img src="docs/images/tui-realm.svg" alt="logo" width="256" height="256" />
</p>

<p align="center">~ A ratatui framework inspired by Elm and React ~</p>
<p align="center">
  <a href="docs/en/get-started.md" target="_blank">Get started</a>
  ·
  <a href="https://github.com/veeso/tui-realm-stdlib" target="_blank">Standard Library</a>
  ·
  <a href="https://docs.rs/tuirealm" target="_blank">Documentation</a>
</p>

<p align="center">Developed by <a href="https://veeso.github.io/" target="_blank">@veeso</a></p>
<p align="center">Current version: 3.0.1 (09/06/2025)</p>

<p align="center">
  <a href="https://opensource.org/licenses/MIT"
    ><img
      src="https://img.shields.io/badge/License-MIT-teal.svg"
      alt="License-MIT"
  /></a>
  <a href="https://github.com/veeso/tui-realm/stargazers"
    ><img
      src="https://img.shields.io/github/stars/veeso/tui-realm.svg?style=plain"
      alt="Repo stars"
  /></a>
  <a href="https://crates.io/crates/tuirealm"
    ><img
      src="https://img.shields.io/crates/d/tuirealm.svg"
      alt="Downloads counter"
  /></a>
  <a href="https://crates.io/crates/tuirealm"
    ><img
      src="https://img.shields.io/crates/v/tuirealm.svg"
      alt="Latest version"
  /></a>
  <a href="https://ko-fi.com/veeso">
    <img
      src="https://img.shields.io/badge/donate-ko--fi-red"
      alt="Ko-fi"
  /></a>
</p>
<p align="center">
<a href="https://github.com/veeso/tui-realm/actions/workflows/ratatui_crossterm.yml"
    ><img
      src="https://github.com/veeso/tui-realm/actions/workflows/ratatui_crossterm.yml/badge.svg"
      alt="Ratatui-Crossterm CI"
  /></a>
  <a href="https://github.com/veeso/tui-realm/actions/workflows/ratatui_termion.yml"
    ><img
      src="https://github.com/veeso/tui-realm/actions/workflows/ratatui_termion.yml/badge.svg"
      alt="Ratatui-Termion CI"
  /></a>
  <a href="https://github.com/veeso/tui-realm/actions/workflows/crossterm-windows.yml"
    ><img
      src="https://github.com/veeso/tui-realm/actions/workflows/crossterm-windows.yml/badge.svg"
      alt="Crossterm CI (Windows)"
  /></a>
  <a href="https://coveralls.io/github/veeso/tui-realm"
    ><img
      src="https://coveralls.io/repos/github/veeso/tui-realm/badge.svg"
      alt="Coveralls"
  /></a>
  <a href="https://docs.rs/tuirealm"
    ><img
      src="https://docs.rs/tuirealm/badge.svg"
      alt="Docs"
  /></a>
</p>

---

- [tui-realm](#tui-realm)
  - [About tui-realm 👑](#about-tui-realm-)
  - [Features 🎁](#features-)
  - [Get started 🏁](#get-started-)
    - [Add tui-realm to your Cargo.toml 🦀](#add-tui-realm-to-your-cargotoml-)
      - [Enabling other backends ⚠️](#enabling-other-backends-️)
    - [Create a tui-realm application 🪂](#create-a-tui-realm-application-)
    - [Run examples 🔍](#run-examples-)
  - [Standard components library 🎨](#standard-components-library-)
  - [Community components 🏘️](#community-components-️)
  - [Guides 🎓](#guides-)
  - [Documentation 📚](#documentation-)
  - [Apps using tui-realm 🚀](#apps-using-tui-realm-)
  - [Support the developer ☕](#support-the-developer-)
  - [Contributing and issues 🤝🏻](#contributing-and-issues-)
  - [Changelog ⏳](#changelog-)
  - [License 📃](#license-)

---

## About tui-realm 👑

tui-realm is a **framework** for **[ratatui](https://github.com/ratatui-org/ratatui)** to simplify the implementation of terminal user interfaces adding the possibility to work with re-usable components with properties and states, as you'd do in React. But that's not all: the components communicate with the ui engine via a system based on **Messages** and **Events**, providing you with the possibility to implement `update` routines as happens in Elm. In addition, the components are organized inside the **View**, which manages mounting/umounting, focus and event forwarding for you.

And that also explains the reason of the name: **Realm stands for React and Elm**.

tui-realm also comes with a standard library of components, which can be added to your dependencies, that you may find very useful. Don't worry, they are optional if you don't want to use them 😉, just follow the guide in [get started](#get-started-).

![Demo](/docs/images/demo.gif)

See tui-realm in action in the [Example](#run-examples-) or if you want to read more about tui-realm start reading the official guide [HERE](docs/en/get-started.md).

## Features 🎁

- ⌨️ **Event-driven**
- ⚛️ Based on **React** and **Elm**
- 🍲 **Boilerplate** code
- 🚀 Quick-setup
- 🎯 Single **focus** and **states** management
- 🙂 Easy to learn
- 🤖 Adaptable to any use case

---

## Get started 🏁

> ⚠️ Warning: currently tui-realm supports these backends: crossterm, termion

### Add tui-realm to your Cargo.toml 🦀

If you want the default features, just add tuirealm 1.x version:

```toml
tuirealm = "3"
```

otherwise you can specify the features you want to add:

```toml
tuirealm = { version = "3", default-features = false, features = [ "derive", "serialize", "termion" ] }
```

Supported features are:

- `derive` (*default*): add the `#[derive(MockComponent)]` proc macro to automatically implement `MockComponent` for `Component`. [Read more](https://github.com/veeso/tuirealm_derive).
- `serialize`: add the serialize/deserialize trait implementation for `KeyEvent` and `Key`.
- `crossterm`: use the [crossterm](https://github.com/crossterm-rs/crossterm) terminal backend
- `termion`: use the [termion](https://github.com/redox-os/termion) terminal backend

#### Enabling other backends ⚠️

This library supports two backends: `crossterm` and `termion`, and two high
level terminal TUI libraries: `tui` and `ratatui`. Whenever you explicitly
declare any of the TUI library or backend feature sets you should disable the
crate's default features.

> ❗ The two features can co-exist, even if it doesn't make too much sense.

Example using crossterm:

```toml
tuirealm = { version = "3", default-features = false, features = [ "derive", "crossterm" ]}
```

Example using the termion backend:

```toml
tuirealm = { version = "3", default-features = false, features = [ "derive", "termion" ] }
```

### Create a tui-realm application 🪂

View how to implement a tui-realm application in the [related guide](/docs/en/get-started.md).

### Run examples 🔍

Still confused about how tui-realm works? Don't worry, try with the examples:

- [demo](/examples/demo/demo.rs): a simple application which shows how tui-realm works

    ```sh
    cargo run --example demo
    ```

---

## Standard components library 🎨

Tui-realm comes with an optional standard library of components I thought would have been useful for most of the applications.
If you want to use it, just add the [tui-realm-stdlib](https://github.com/veeso/tui-realm-stdlib) to your `Cargo.toml` dependencies.

## Community components 🏘️

These components are not included in tui-realm, but have been developed by other users. I like advertising other's contents, so here you can find a list of components you may find useful for your next tui-realm project 💜.

- [tui-realm-textarea](https://github.com/veeso/tui-realm-textarea) A textarea/editor component developed by [@veeso](https://github.com/veeso)
- [tui-realm-treeview](https://github.com/veeso/tui-realm-treeview) A treeview component developed by [@veeso](https://github.com/veeso)

Want to add yours? Open an issue using the `New app/component` template 😄

---

## Guides 🎓

- [Get Started Guide](/docs/en/get-started.md)
- [Advanced concepts](/docs/en/advanced.md)

---

## Documentation 📚

The developer documentation can be found on Rust Docs at <https://docs.rs/tuirealm>

---

## Apps using tui-realm 🚀

- [BugStalker](https://github.com/godzie44/BugStalker)
- [cliflux](https://github.com/spencerwi/cliflux)
- [csvs](https://github.com/koma-private/csvs)
- [donmaze](https://github.com/veeso/donmaze)
- [matrix-rust-sdk](https://github.com/matrix-org/matrix-rust-sdk)
- [paat](https://github.com/ebakoba/paat)
- [termusic](https://github.com/tramhao/termusic)
- [termscp](https://github.com/veeso/termscp)
- [tisq](https://crates.io/crates/tisq)
- [todotui](https://github.com/newfla/todotui)
- [tuifeed](https://github.com/veeso/tuifeed)
- [turdle](https://crates.io/crates/turdle)

Want to add yours? Open an issue using the `New app/component` template 😄

---

## Support the developer ☕

If you like tui-realm and you're grateful for the work I've done, please consider a little donation 🥳

You can make a donation with one of these platforms:

[![ko-fi](https://img.shields.io/badge/Ko--fi-F16061?style=for-the-badge&logo=ko-fi&logoColor=white)](https://ko-fi.com/veeso)
[![PayPal](https://img.shields.io/badge/PayPal-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://www.paypal.me/chrisintin)

---

## Contributing and issues 🤝🏻

Contributions, bug reports, new features and questions are welcome! 😉
If you have any question or concern, or you want to suggest a new feature, or you want just want to improve tui-realm, feel free to open an issue or a PR.

Please follow [our contributing guidelines](CONTRIBUTING.md)

---

## Changelog ⏳

View tui-realm's changelog [HERE](CHANGELOG.md)

---

## License 📃

tui-realm is licensed under the MIT license.

You can read the entire license [HERE](LICENSE)
