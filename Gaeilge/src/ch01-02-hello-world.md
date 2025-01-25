## Dia duit, a Dhomhanda!

Anois go bhfuil Rust suiteáilte agat, tá sé in am do chéad chlár Rust a scríobh.
Tá sé traidisiúnta agus tú ag foghlaim teanga nua clár beag a scríobh
priontaí an téacs `Dia duit, domhan!` ar an scáileán, mar sin déanfaimid an rud céanna anseo!

> Nóta: Glacann an leabhar seo le cur amach bunúsach ar an líne ordaithe. Déanann Rust
> níl aon éileamh ar d'eagarthóireacht nó d'uirlisiú nó cá bhfuil cónaí ar do chód, mar sin de
> más fearr leat timpeallacht forbartha comhtháite (IDE) a úsáid ina ionad
> an líne ordaithe, bíodh leisce ort an IDE is fearr leat a úsáid. Tá roinnt IDEanna anois
> méid na tacaíochta Rust; seiceáil doiciméadú an IDE le haghaidh sonraí.
> tá an Rust fhoireann ag díriú ar thacaíocht iontach IDE a chumasú trí `rust-analyzer`. Féach
> [Aguisín D][devtools]<!-- neamhaird --> le haghaidh tuilleadh sonraí.

### Eolaire Tionscadal á Chruthú

Tosóidh tú trí eolaire a dhéanamh chun do chód Rust a stóráil. Is cuma
go Rust áit a bhfuil cónaí ar do chód, ach do na cleachtaí agus na tionscadail sa leabhar seo,
molaimid eolaire _tionscadail_ a dhéanamh i do eolaire baile agus gach rud a choimeád
do thionscadail ann.

Oscail teirminéal agus cuir isteach na horduithe seo a leanas chun eolaire _tionscadail_ a dhéanamh
agus eolaire don "Dia duit, an domhan!" tionscadal laistigh den eolaire _tionscadail_.

Le haghaidh Linux, macOS, agus PowerShell ar Windows, cuir isteach é seo:

```console
$ mkdir ~/tionscadail
$ cd ~/tionscadail
$ mkdir hello_world
$ cd hello_world
```

I gcás Windows CMD, cuir isteach é seo:

```cmd
> mkdir "%USERPROFILE%\tionscadail"
> cd /d "%USERPROFILE%\tionscadail"
> mkdir hello_world
> cd hello_world
```

### Clár Rust á Scríobh agus á Rith

Ansin, déan comhad foinse nua agus glaoigh air _main.rs_. Comhaid Rust deireadh i gcónaí le
an síneadh _.rs_. Má tá níos mó ná focal amháin in úsáid agat i d’ainm comhaid, beidh an
Is é an gnás foscór a úsáid chun iad a scaradh. Mar shampla, úsáid
_hello_world.rs_ seachas _helloworld.rs_.

Anois oscail an comhad _main.rs_ a chruthaigh tú díreach agus cuir isteach an cód i Liostú 1-1.

<Listing number="1-1" file-name="main.rs" caption="Clár a phriontálann `Dia duit, a shaoghail!`">

```rust
fn main() {
    println!("Dia duit, domhan!");
}
```

</Listing>

Sábháil an comhad agus téigh ar ais go dtí do fhuinneog teirminéil sa
\_~/tionscadail/hello_world eolaire. Ar Linux nó macOS, cuir isteach an méid seo a leanas
orduithe chun an comhad a thiomsú agus a rith:

```consól
$ rustc main.rs
$ ./main
Dia duit, domhan!
```

Ar Windows, cuir isteach an t-ordú `.\main.exe` in ionad `./main`:

```powershell
> rustc main.rs
> .\main.exe
Dia duit, domhan!
```

beag beann ar do chóras oibriúcháin, ba chóir an teaghrán `Dia duit, a Dhomhan!` a phriontáil go dtí
an teirminéal. Mura bhfeiceann tú an t-aschur seo, féach ar ais chuig an
[“Fabhtcheartú”][fabhtcheartú]<!-- neamhaird a dhéanamh ar --> cuid den Suiteáil
alt le haghaidh bealaí chun cabhair a fháil.

Má rinne `Dia duit, a domhan!` cló, comhghairdeas! Tá Rust scríofa agat go hoifigiúil
clár. Déanann sé sin ríomhchláraitheoir Rust duit - fáilte romhat!

### Anatamaíocht Chlár Rust

Déanaimis athbhreithniú ar seo "Dia duit, a domhan!" clár go mion. Seo chugaibh an chéad píosa
an puzal:

```rust
fn main() {

}
```

Sainmhíníonn na línte seo feidhm darb ainm `main`. Tá an fheidhm `main` speisialta: é
i gcónaí ar an gcéad chód a ritheann i ngach clár inrite Rust. Anseo, an
dearbhaíonn an chéad líne feidhm darb ainm `main` nach bhfuil paraiméadair agus tuairisceáin ann
faic. Dá mbeadh paraiméadair ann, rachadh siad laistigh de na lúibíní `()`.

Tá corp na feidhme fillte i `{}`. Éilíonn Rust lúibíní curly timpeall ar fad
comhlachtaí feidhm. Is stíl mhaith é an lúibín cuartha tosaigh a chur ar an gcéanna
líne mar dhearbhú feidhme, ag cur spás amháin eatarthu.

> Nóta: Más mian leat cloí le stíl chaighdeánach ar fud na dtionscadal Rust, is féidir leat
> bain úsáid as uirlis uathfhormáidithe ar a dtugtar `rustfmt` chun do chód a fhormáidiú in a
> stíl ar leith (tuilleadh ar `rustfmt` in
> [Aguisín D][devtools]<!-- neamhaird a dhéanamh -->). Tá an uirlis seo curtha san áireamh ag foireann Rust
> leis an dáileadh caighdeánach Rust, mar is é `rustc`, mar sin ba chóir go mbeadh sé cheana féin
> suiteáilte ar do ríomhaire!

Tá an cód seo a leanas i gcorp na `main`:

```rust
println!("Dia duit, a domhan!");
```

Déanann an líne seo an obair ar fad sa chlár beag seo: priontaí sí téacs chuig an
scáileán. Tá ceithre shonraí tábhachtacha le tabhairt faoi deara anseo.

Ar dtús, glaonn `println!` macra Rust. Dá mba rud é gur ghlaoigh sé feidhm ina hionad, is é
chuirfí isteach mar `println` (gan an `!`). Pléifimid macraí Rust in
níos mó sonraí i gCaibidil 20. Faoi láthair, ní gá duit ach fios a bheith agat go n-úsáideann tú `!`
Ciallaíonn sé sin go bhfuil tú ag glaoch ar mhacra in ionad gnáthfheidhm agus na macraí sin
ná lean na rialacha céanna le feidhmeanna i gcónaí.

Ar an dara dul síos, feiceann tú an teaghrán `"Dia duit, domhan!"`. Gabhaimid an teaghrán seo mar argóint
go `println!`, agus clóitear an teaghrán go dtí an scáileán.

Sa tríú háit, deireadh muid an líne le leathstad (`;`), a léiríonn go bhfuil sé seo
tá deireadh le cur in iúl agus tá an chéad cheann eile réidh le tosú. An chuid is mó de na línte de chód Rust
deireadh le leathstad.

### Is Céimeanna ar Leith iad Tiomsú agus Rith

Tá clár nuachruthaithe díreach á rith agat, mar sin déanaimis scrúdú ar gach céim sa
próiseas.

Sula ritheann tú clár Rust, ní mór duit é a thiomsú ag baint úsáide as an tiomsaitheoir Rust trí
an t-ordú `rustc` a iontráil agus ainm do chomhaid foinse a thabhairt dó, mar
seo:

```console
$ rustc main.rs
```

Má tá cúlra C nó C++ agat, tabharfaidh tú faoi deara go bhfuil sé seo cosúil le `gc`
nó `clang`. Tar éis a thiomsú go rathúil, aschuir Rust inrite dénártha.

Ar Linux, macOS, agus PowerShell ar Windows, is féidir leat an inrite a fheiceáil le
ag dul isteach an t-ordú `ls` i do bhlaosc:

```console
$ ls
main  main.rs
```

Ar Linux agus macOS, feicfidh tú dhá chomhad. Le PowerShell ar Windows, déanfaidh tú
féach ar na trí chomhad chéanna a d'fheicfeá ag baint úsáide as CMD. Le CMD ar Windows, tú
chuirfeadh sé seo a leanas isteach:

```cmd
> dir /B %= deir an rogha /B gan ach ainmneacha na gcomhad a thaispeáint =%
main.exe
main.pdb
main.rs
```

Taispeánann sé seo an comhad cód foinse leis an síneadh _.rs_, an comhad inrite
(_main.exe_ ar Windows, ach _main_ ar gach ardán eile), agus, nuair a úsáid
Windows, comhad ina bhfuil faisnéis dífhabhtaithe leis an iarmhír _.pdb_.
As seo, ritheann tú an comhad _main_ nó _main.exe_, mar seo:

```console
$ ./main # or .\main.exe ar Windows
```

Más é do _main.rs_ do "Dia duit, domhan!" clár, priontaí an líne seo `Dia duit,
domhan!` chuig do chríochfort.

Má tá níos mó eolas agat ar theanga dhinimiciúil, mar Ruby, Python, nó
JavaScript, seans nach bhfuil tú cleachta le clár a thiomsú agus a rith mar
céimeanna ar leith. Is teanga tiomsaithe _roimh-ama_ é Rust, rud a chiallaíonn gur féidir leat
clár a thiomsú agus an inrite a thabhairt do dhuine eile, agus is féidir leo é a rith
fiú gan Rust a bheith suiteáilte. Má thugann tú _.rb_, _.py_, nó
_.js_, ní mór cur i bhfeidhm Ruby, Python nó JavaScript a bheith acu
suiteáilte (faoi seach). Ach sna teangacha sin, níl uait ach ordú amháin chun
do chlár a thiomsú agus a rith. Is malairt-uaire é gach rud i ndearadh teanga.

Tá sé ceart go leor ach le `rustc` a thiomsú do chláir shimplí, ach mar do thionscadal
fás, beidh tú ag iarraidh na roghanna go léir a bhainistiú agus é a dhéanamh éasca do chuid a roinnt
cód. Ansin, cuirfimid an uirlis lasta in aithne duit, a chabhróidh leat scríobh
cláir Rust domhan fíor.

[fabhtcheartú]: ch01-01-installation.html#troubleshooting
[devtools]: appendix-04-useful-development-tools.html
