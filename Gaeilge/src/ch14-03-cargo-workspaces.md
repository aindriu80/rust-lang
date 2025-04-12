## Spásanna Oibre Cargo

I gCaibidil 12, thógamar pacáiste a chuimsigh cliathbhosca dénártha agus leabharlann
cliathbhosca. De réir mar a théann do thionscadal chun cinn, seans go bhfaighidh tú an crate leabharlainne
ag éirí níos mó fós agus ba mhaith leat do phacáiste a roinnt níos faide isteach
crates leabharlann il. Cuireann Cargo gné ar a dtugtar _workspaces_ ar fáil ar féidir
cabhrú le ilphacáistí gaolmhara a fhorbraítear in éineacht.

### Spás Oibre á Chruthú

Is é atá i _workspace_ ná sraith pacáistí a roinneann an _Cargo.lock_ céanna agus an t-aschur céanna
eolaire. Déanaimis tionscadal ag baint úsáide as spás oibre - úsáidfimid cód fánach mar sin déanfaimid
is féidir díriú ar struchtúr an spáis oibre. Tá bealaí éagsúla chun
spás oibre a struchtúrú, mar sin ní léireoimid ach bealach coiteann amháin. Beidh a
spás oibre ina bhfuil dénártha agus dhá leabharlann. An dénártha, a sholáthróidh
an phríomhfheidhmíocht, ag brath ar an dá leabharlann. Beidh leabharlann amháin
cuir feidhm `add_one` ar fáil, agus feidhm `add_two` leis an dara leabharlann.
Beidh na trí chliathbhosca seo mar chuid den spás oibre céanna. Tosóimid ag cruthú
eolaire nua don spás oibre:

```console
$ mkdir add
$ cd add
```

Ansin, san eolaire _add_, cruthaímid an comhad _Cargo.toml_ a dhéanfaidh
cumraigh an spás oibre ar fad. Ní bheidh alt `[package]` ag an gcomhad seo.
Ina áit sin, tosóidh sé le rannán `[workspace]` a ligfidh dúinn cur leis
baill chuig an spás oibre. Déanaimid pointe freisin chun an ceann is déanaí agus is mó a úsáid
leagan de algartam réitithe Cargo inár spás oibre tríd an
`resolver` go `"2"`.

<span class="filename">Ainm comhaid: Cargo.toml</span>

```toml
{{#include ../../listings/ch14-more-about-cargo/no-listing-01-workspace/add/Cargo.toml}}
```

Ansin, cruthóimid an gcliathbhosca dénártha `adder` trí `cargo new` a rith laistigh den
_cuir_ eolaire:

<!-- athghiniúint de láimh
liostaí cd/ch14-tuilleadh-faoi-lasta/aschur-amháin-01-adder-crate/add
rm -rf adder
adder nua lasta
cóip den aschur thíos
-->

```console
$ cargo new adder
    Creating binary (application) `adder` package
      Adding `adder` as member of workspace at `file:///projects/add`
```

Nuair a ritheann `cargo new` taobh istigh de spás oibre cuireann sé go huathoibríoch leis an nuachruthaithe
pacáiste chuig an eochair `members` sa sainmhíniú `[workspace]` sa spás oibre
`Cargo.toml`, mar seo:

```toml
{{#include ../../listings/ch14-more-about-cargo/output-only-01-adder-crate/add/Cargo.toml}}
```

Ag an bpointe seo, is féidir linn an spás oibre a thógáil trí `cargo build` a reáchtáil. Na comhaid
ba cheart go mbeadh cuma mar seo i do _add_ eolaire:

```text
├── Cargo.lock
├── Cargo.toml
├── adder
│   ├── Cargo.toml
│   └── src
│       └── main.rs
└── target
```

Tá eolaire _target_ amháin sa spás oibre ar an leibhéal is airde a tiomsaíodh
cuirfear artifacts isteach; níl a chuid féin ag an bpacáiste `adder`
_target_ eolaire. Fiú dá mbeadh muid chun `cargo build` a rith ón taobh istigh den
_adder_ eolaire, bheadh ​​na déantáin tiomsaithe fós i _add/target_
seachas _add/adder/target_. Struchtúraíonn Cargo an t-eolaire _target_ i
spás oibre mar seo mar go bhfuil na crates i spás oibre i gceist a bheith ag brath ar
chéile. Dá mbeadh a eolaire _target_ féin ag gach cliathbhosca, bheadh ​​ag gach cliathbhosca
chun gach ceann de na crates eile sa spás oibre a ath-thiomsú chun na déantáin a chur
ina _target_ eolaire féin. Trí chomhadlann _target_ amháin a roinnt, na crates
is féidir atógáil gan ghá a sheachaint.

### An Dara Pacáiste a Chruthú sa Spás Oibre

Ansin, cruthaímid pacáiste ball eile sa spás oibre agus cuirfimid glaoch air
`add_one` leis. Athraigh an barrleibhéal _Cargo.toml_ chun an cosán _add_one_ a shonrú
liosta na `members`:

<span class="filename">Ainm comhaid: Cargo.toml</span>

```toml
{{#include ../../listings/ch14-more-about-cargo/no-listing-02-workspace-with-two-crates/add/Cargo.toml}}
```

Ansin ginigh cliathbhosca leabharlainne nua darb ainm `add_one`:

<!-- athghiniúint de láimh
liostaí cd/ch14-níos mó faoi-lasta/aschur-amháin-02-cuir-amháin/cuir leis
rm -rf add_one
lasta add_one nua --lib
cóip den aschur thíos
-->

```consól
$cargo add_one nua --lib
 Leabharlann á chruthú pacáiste `add_one`
 Ag cur `add_one` isteach mar bhall den spás oibre ag `comhad:///projects/add`
```

Ba cheart go mbeadh na heolairí agus na comhaid seo i do chomhadlann _add_ anois:

```téacs
├── Cargo.lock
├── Cargo.toml
├── add_one
│ ├── Cargo.toml
│ └── src
│ └── lib.rs
├── nathair
│ ├── Cargo.toml
│ └── src
│ └── príomh.rs
└── sprioc
```

Sa chomhad _add_one/src/lib.rs_, cuirimis feidhm `add_one` leis:

<span class="filename">Ainm comhaid: add_one/src/lib.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch14-more-about-cargo/no-listing-02-workspace-with-two-crates/add/add_one/src/lib.rs}}
```

Anois is féidir linn an pacáiste ` adder` a bheith againn lenár dénártha ag brath ar an `add_one`
pacáiste a bhfuil ár leabharlann. Ar dtús, ní mór dúinn spleáchas cosán a chur leis
`add_one` le _adder/Cargo.toml_.

<span class="filename">Ainm comhaid: adder/Cargo.toml</span>

```toml
{{#include ../../listings/ch14-more-about-cargo/no-listing-02-workspace-with-two-crates/add/adder/Cargo.toml:6:7}}
```

Ní ghlacann Cargo leis go mbeidh crates i spás oibre ag brath ar a chéile, mar sin de
ní mór dúinn a bheith soiléir faoi na caidrimh spleáchais.

Ansin, bainimis úsáid as an bhfeidhm `add_one` (ón gcliathbhosca `add_one`) sa
cliathbhosca `adder`. Oscail an comhad _adder/src/main.rs_ agus athraigh an `main`
feidhm chun an fheidhm `add_one` a ghlaoch, mar atá i Liostú 14-7.

<Listing number="14-7" file-name="adder/src/main.rs" caption="Ag baint úsáide as an gcliathbhosca leabharlainne `add_one` i gcliathbhosca `adder`">

```rust,ignore
{{#rustdoc_include ../../listings/ch14-more-about-cargo/listing-14-07/add/adder/src/main.rs}}
```

</Listing>

Déanaimis an spás oibre a thógáil trí `cargo build` a rith sa bharrleibhéal _add_
eolaire!

<!-- athghiniúint de láimh
liostaí cd/ch14-more-about-cargo/listing-14-07/add
tógáil lasta
aschur cóip thíos; ní láimhseálann an script nuashonraithe aschuir fochomhadlanna i gcosáin i gceart
-->

```console
$ cargo build
   Compiling add_one v0.1.0 (file:///projects/add/add_one)
   Compiling adder v0.1.0 (file:///projects/add/adder)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.22s
```

Chun an cliathbhosca dénártha a rith ón eolaire _add_, is féidir linn a shonrú cé acu
pacáiste sa spás oibre ba mhaith linn a rith tríd an argóint `-p` agus an
ainm an phacáiste le `cargo run`:

<!-- athghiniúint de láimh
liostaí cd/ch14-more-about-cargo/listing-14-07/add
rith lasta -p adder
aschur cóip thíos; ní láimhseálann an script nuashonraithe aschuir fochomhadlanna i gcosáin i gceart
-->

```console
$ cargo run -p adder
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.00s
     Running `target/debug/adder`
Hello, world! 10 plus one is 11!
```

Ritheann sé seo an cód in _adder/src/main.rs_, atá ag brath ar an gcliathbhosca `add_one`.

#### Ag brath ar Phacáiste Seachtrach i Spás Oibre

Tabhair faoi deara nach bhfuil ach comhad _Cargo.lock_ amháin ag an mbarrleibhéal,
seachas _Cargo.lock_ a bheith i gcomhadlann gach cliathbhosca. Cinntíonn sé seo go
tá na crates go léir ag baint úsáide as an leagan céanna de gach spleáchas. Má chuirimid an `rand`
pacáiste chuig na comhaid _adder/Cargo.toml_ agus _add_one/Cargo.toml_, déanfaidh Cargo
Réitigh an dá cheann go leagan amháin de `rand` agus taifead é sin sa cheann
_Cargo.glas_. Má dhéantar na crates go léir sa spás oibre, bain úsáid as na spleáchais chéanna
ciallaíonn sé seo go mbeidh na crates ag luí lena chéile i gcónaí. Cuirimis an
cliathbhosca `rand` chuig an rannán `[dependencies]` sa chomhad _add_one/Cargo.toml_
ionas gur féidir linn an cliathbhosca `rand` a úsáid sa crate `add_one`:

<!-- Agus an leagan de `rand` á nuashonrú, nuashonraigh an leagan de
úsáidtear `rand` sna comhaid seo ionas go dtagann siad go léir le:
* ch02-00-buille faoi thuairim-cluiche-tutorial.md
*ch07-04-ag tabhairt-cosáin-i--scóip-leis-an-úsáid-eochairfhocal.md
-->

<span class="filename">Ainm comhaid: add_one/Cargo.toml</span>

```toml
{{#include ../../listings/ch14-more-about-cargo/no-listing-03-workspace-with-external-dependency/add/add_one/Cargo.toml:6:7}}
```

Is féidir linn `use rand;` a chur leis an gcomhad _add_one/src/lib.rs_ anois, agus an
spás oibre iomlán trí `cargo build` a rith san eolaire _add_ a thabhairt isteach
agus an gcliathbhosca `rand` a thiomsú. Gheobhaidh muid rabhadh amháin mar nílimid
ag tagairt don `rand` a thugamar isteach sa scóip:

<!-- manual-regeneration
cd listings/ch14-more-about-cargo/no-listing-03-workspace-with-external-dependency/add
cargo build
copy output below; the output updating script doesn't handle subdirectories in paths properly
-->

```console
$ cargo build
    Updating crates.io index
  Downloaded rand v0.8.5
   --snip--
   Compiling rand v0.8.5
   Compiling add_one v0.1.0 (file:///projects/add/add_one)
warning: unused import: `rand`
 --> add_one/src/lib.rs:1:5
  |
1 | use rand;
  |     ^^^^
  |
  = note: `#[warn(unused_imports)]` on by default

warning: `add_one` (lib) generated 1 warning (run `cargo fix --lib -p add_one` to apply 1 suggestion)
   Compiling adder v0.1.0 (file:///projects/add/adder)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.95s
```

Tá faisnéis sa _Cargo.lock_ barrleibhéil anois faoi spleáchas na
`add_one` ar `rand`. Mar sin féin, cé go n-úsáidtear `rand` áit éigin sa
spás oibre, ní féidir linn é a úsáid i crates eile sa spás oibre mura gcuirimid leis
`rand` chuig a gcuid comhad _Cargo.toml_ freisin. Mar shampla, má chuirimid `use rand;` leis
chuig an gcomhad _adder/src/main.rs_ don phacáiste `adder`, gheobhaidh muid earráid:

<!-- manual-regeneration
cd listings/ch14-more-about-cargo/output-only-03-use-rand/add
cargo build
copy output below; the output updating script doesn't handle subdirectories in paths properly
-->

```console
$ cargo build
  --snip--
   Compiling adder v0.1.0 (file:///projects/add/adder)
error[E0432]: unresolved import `rand`
 --> adder/src/main.rs:2:5
  |
2 | use rand;
  |     ^^^^ no external crate `rand`
```

Chun é seo a shocrú, cuir an comhad _Cargo.toml_ in eagar don phacáiste `adder` agus cuir in iúl
go bhfuil `rand` ina spleáchas dó freisin. Déanfar an pacáiste `adder` a thógáil
cuir `rand` leis an liosta spleáchais do `adder` in _Cargo.lock_, ach níl
íoslódálfar cóipeanna breise de `rand`. Cinnteoidh Cargo go mbeidh gach
cliathbhosca i ngach pacáiste sa spás oibre a bheidh in úsáid ag an bpacáiste `rand`
an leagan céanna chomh fada agus a shonraíonn siad leaganacha comhoiriúnacha de `rand`, ag sábháil
spás dúinn agus a chinntiú go mbeidh na crates sa spás oibre ag luí leis
chéile.

Má shonraíonn crates sa spás oibre leaganacha neamh-chomhoiriúnacha den spleáchas céanna,
Réiteoidh Cargo gach ceann acu, ach déanfaidh sé iarracht fós gan ach cúpla leagan a réiteach
agus is féidir.

#### Tástáil á Chur le Spás Oibre

Le feabhsú eile, cuirimis tástáil ar an bhfeidhm `add_one::add_one` laistigh den crate `add_one`:

<span class="filename">Filename: add_one/src/lib.rs</span>

```rust,noplayground
{{#rustdoc_include ../../listings/ch14-more-about-cargo/no-listing-04-workspace-with-tests/add/add_one/src/lib.rs}}
```

Anois reáchtáil `cargo test` san eolaire _add_ barrleibhéil. Rith `cargo test` isteach
reáchtálfar spás oibre struchtúrtha mar seo na trialacha do na crates ar fad i
an spás oibre:

<!-- manual-regeneration
cd listings/ch14-more-about-cargo/no-listing-04-workspace-with-tests/add
cargo test
copy output below; the output updating script doesn't handle subdirectories in
paths properly
-->

```console
$ cargo test
   Compiling add_one v0.1.0 (file:///projects/add/add_one)
   Compiling adder v0.1.0 (file:///projects/add/adder)
    Finished `test` profile [unoptimized + debuginfo] target(s) in 0.20s
     Running unittests src/lib.rs (target/debug/deps/add_one-f0253159197f7841)

running 1 test
test tests::it_works ... ok

test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

     Running unittests src/main.rs (target/debug/deps/adder-49979ff40686fa8e)

running 0 tests

test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

   Doc-tests add_one

running 0 tests

test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s
```

Léiríonn an chéad chuid den aschur go bhfuil an tástáil `it_works` sa `add_one`
cliathbhosca a rith. Léiríonn an chéad chuid eile nach bhfuarthas tástálacha nialais sa `adder`
gcliathbhosca, agus ansin taispeánann an t-alt deireanach náid tástálacha doiciméadú a fuarthas i
an gcliathbhosca `add_one`.

Is féidir linn tástálacha a reáchtáil freisin le haghaidh cliathbhosca ar leith amháin i spás oibre ón
eolaire barrleibhéil tríd an mbratach `-p` a úsáid agus ainm an chliabháin a shonrú
ba mhaith linn tástáil a dhéanamh:

<!-- manual-regeneration
cd listings/ch14-more-about-cargo/no-listing-04-workspace-with-tests/add
cargo test -p add_one
copy output below; the output updating script doesn't handle subdirectories in paths properly
-->

```console
$ cargo test -p add_one
    Finished `test` profile [unoptimized + debuginfo] target(s) in 0.00s
     Running unittests src/lib.rs (target/debug/deps/add_one-b3235fea9a156f74)

running 1 test
test tests::it_works ... ok

test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

   Doc-tests add_one

running 0 tests

test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s
```

Léiríonn an t-aschur seo nach ndearna `cargo test` ach na tástálacha don crate `add_one`  agus
níor rith na tástálacha crate `adder`.

Má fhoilsíonn tú na crates sa spás oibre chuig [crates.io](https://crates.io/),
ní mór gach cliathbhosca sa spás oibre a fhoilsiú ar leithligh. Cosúil le `cargo test`, is féidir linn cliathbhosca ar leith a fhoilsiú inár spás oibre trí úsáid a bhaint as an `-p`
bratach agus ag sonrú ainm an chliathbhosca ba mhaith linn a fhoilsiú.

Chun cleachtadh breise a fháil, cuir crate `cuir_two` leis an spás oibre seo i gceann cosúil leis
mar an crate `add_one`!

De réir mar a fhásann do thionscadal, smaoinigh ar spás oibre a úsáid: is fusa é a thuiscint
comhpháirteanna aonair níos lú ná blob mór cód. Ina theannta sin, a choinneáil
is féidir leis na crates i spás oibre comhordú idir crates a dhéanamh níos éasca má bhíonn siad
a athrú go minic ag an am céanna.
