<!-- Old link, do not remove -->

<a id="installing-binaries-from-cratesio-with-cargo-install"></a>

## Dénártha a shuiteáil le `cargo install`

Ligeann an t-ordú `shuiteáil lasta` duit cliathbhoscaí dénártha a shuiteáil agus a úsáid
go háitiúil. Níl sé seo beartaithe chun pacáistí córais a athsholáthar; tá sé i gceist a
bealach áisiúil d'fhorbróirí Rust uirlisí a shuiteáil a bhfuil daoine eile roinnte orthu
[crates.io]( https://crates.io/) <!-- neamhaird -->. Tabhair faoi deara nach féidir leat ach a shuiteáil
pacáistí a bhfuil spriocanna dénártha acu. Is é sprioc _dhénártha_ an clár inrite
cruthaítear é sin má tá comhad _src/main.rs_ nó comhad eile sonraithe ag an gcliathbhosca
mar dhénártha, i gcomparáid le sprioc leabharlainne nach féidir a rith leis féin ach
oiriúnach lena n-áirítear laistigh de chláir eile. De ghnáth, tá cliathbhoscaí
faisnéis sa chomhad _README_ faoi cé acu an leabharlann é cliathbhosca, an bhfuil a
sprioc dhénártha, nó an dá cheann.

Stóráiltear gach dénártha atá suiteáilte le `cargo install` sa suiteáil
fillteán _bin_ an fhréamh. Má shuiteáil tú Rust ag baint úsáide as _rustup.rs_ agus nach bhfuil aon cheann agat
cumraíochtaí saincheaptha, beidh an eolaire seo *$HOME/.cargo/bin*. Cinntigh go
tá an t-eolaire i do `$PATH` le go mbeidh tú in ann na cláir atá suiteáilte agat le `cargo install` a rith.

Mar shampla, i gCaibidil 12 luaigh muid go bhfuil cur i bhfeidhm Rust de
an uirlis `grep` ar a dtugtar `ripgrep` chun comhaid a chuardach. Chun `ripgrep` a shuiteáil, ní mór dúinn
is féidir leis an méid seo a leanas a rith:

<!-- manual-regeneration
cargo install something you don't have, copy relevant output below
-->

```console
$ cargo install ripgrep
    Updating crates.io index
  Downloaded ripgrep v13.0.0
  Downloaded 1 crate (243.3 KB) in 0.88s
  Installing ripgrep v13.0.0
--snip--
   Compiling ripgrep v13.0.0
    Finished `release` profile [optimized + debuginfo] target(s) in 10.64s
  Installing ~/.cargo/bin/rg
   Installed package `ripgrep v13.0.0` (executable `rg`)
```

Taispeánann an dara líne go deireanach den aschur suíomh agus ainm an
dénártha suiteáilte, arb é `rg` é i gcás `ripgrep`. Chomh fada leis an
tá an t-eolaire suiteála i do `$PATH`, mar a luadh cheana, is féidir leat
ansin rith `rg --help` agus tosú ag baint úsáide as uirlis níos tapúla, níos meirgeach chun comhaid a chuardach!