## Suiteáil

Is é an chéad chéim ná Rust a shuiteáil. Déanfaimid Rust a íoslódáil trí 'rustup', a
uirlis líne ordaithe chun leaganacha Rust agus uirlisí gaolmhara a bhainistiú. Beidh ort
Nasc Idirlín le haghaidh soghluaiste íoslódáil.

> Nóta: Más fearr leat gan `rustup` a úsáid ar chúis éigin, féach le do thoil an
> [leathanach Modhanna Eile Suiteála Rust][otherinstall] le haghaidh tuilleadh roghanna.

Suiteáil na céimeanna seo a leanas an leagan cobhsaí is déanaí den tiomsaitheoir Rust.
Cinntíonn cobhsaíocht Rust go bhfuil na samplaí go léir sa leabhar a
leanfaidh tiomsú ar aghaidh ag tiomsú le leaganacha Rust níos nuaí. D'fhéadfadh an t-aschur
difríocht beagán idir leaganacha mar is minic a fheabhsaíonn Rust teachtaireachtaí earráide agus
rabhaidh. I bhfocail eile, aon leagan níos nuaí, cobhsaí de Rust a shuiteáil tú ag baint úsáide as
ba chóir go n-oibreodh na céimeanna seo mar a bheifí ag súil leis le hábhar an leabhair seo.

> ### Nodaireacht Líne Ordú
>
> Sa chaibidil seo agus tríd an leabhar, taispeánfaimid roinnt orduithe a úsáidtear sa
> teirminéal. Tosaíonn línte ar chóir duit a chur isteach i teirminéal le `$`. tu
> ní gá an carachtar `$` a chlóscríobh; is é an leid líne ordaithe a thaispeántar do
> cuir in iúl tús gach ordú. Línte nach dtosaíonn le `$` de ghnáth
> taispeáin aschur an ordaithe roimhe seo. Ina theannta sin, PowerShell-shonrach
> úsáidfidh `>` samplaí seachas `$`.

### Suiteáil `rustup` ar Linux nó macOS

Má tá Linux nó macOS á úsáid agat, oscail teirminéal agus cuir isteach an t-ordú seo a leanas:

```console
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

Íoslódálann an t-ordú script agus cuireann sé tús le suiteáil an `rustup`
uirlis, a shuiteálann an leagan cobhsaí is déanaí de Rust. Seans go dtabharfar leid thú
le haghaidh do phasfhocal. Má éiríonn leis an suiteáil, feicfear an líne seo a leanas:

```text
Rust is installed now. Great!
```

Beidh _linker_ ag teastáil uait freisin, ar clár é a úsáideann Rust chun páirt a ghlacadh ann
aschuir tiomsaithe i gcomhad amháin. Is dócha go bhfuil ceann agat cheana féin. Má fhaigheann tú
earráidí nascóirí, ba cheart duit tiomsaitheoir C a shuiteáil, lena n-áireofar de ghnáth a
nascóir. Tá tiomsaitheoir C úsáideach freisin toisc go mbraitheann roinnt pacáistí Rust coitianta
C cód agus beidh tiomsaitheoir C de dhíth.

Ar macOS, is féidir leat tiomsaitheoir C a fháil trí:

```console
$ xcode-select --install
```

Ba cheart go ginearálta d'úsáideoirí Linux GCC nó Clang a shuiteáil, de réir a gcuid
doiciméadú dáileacháin. Mar shampla, má úsáideann tú Ubuntu, is féidir leat a shuiteáil
an pacáiste `build-essential`.

### Suiteáil `rustup` ar Windows

Ar Windows, téigh chuig [https://www.rust-lang.org/tools/install][shuiteáil] agus lean
Treoracha le haghaidh suiteáil Rust. Ag pointe éigin sa suiteáil, déanfaidh tú
a spreagadh chun Visual Studio a shuiteáil. Soláthraíonn sé seo nascóir agus an dúchais
leabharlanna ag teastáil chun cláir a thiomsú. Má theastaíonn tuilleadh cabhrach uait leis an gcéim seo, féach
[https://rust-lang.github.io/rustup/installation/windows-msvc.html][msvc]

Úsáideann an chuid eile den leabhar seo orduithe a oibríonn sa dá _cmd.exe_ agus PowerShell.
Má tá difríochtaí sonracha ann, míneoimid cé acu ba cheart a úsáid.

### Fabhtcheartú

Chun seiceáil an bhfuil Rust suiteáilte i gceart agat, oscail sliogán agus cuir isteach é seo
líne:

```console
$ rustc --version
```

Ba cheart duit uimhir an leagain a fheiceáil, hash a thiomnú agus dáta geallta a dhéanamh ar a dhéanaí
leagan cobhsaí atá eisithe, san fhormáid seo a leanas:

```text
rustc x.y.z (abcabcabc bbbb-mm-ll)
```

Má fheiceann tú an fhaisnéis seo, tá tú tar éis Rust a shuiteáil go rathúil! Mura ndéanann tú
féach an fhaisnéis seo, seiceáil go bhfuil Rust i do athróg córais `% PATH%` mar
leanas.

I Windows CMD, bain úsáid as:

```console
> echo %PATH%
```

I PowerShell, bain úsáid as:

```powershell
> echo $env:Path
```

I Linux agus macOS, bain úsáid as:

```console
$ echo $PATH
```

Má tá sé sin ceart agus nach bhfuil Rust fós ag obair, tá roinnt cinn ann
áiteanna inar féidir leat cabhair a fháil. Faigh amach conas dul i dteagmháil le Rustaceans eile (a
leasainm amaideach a dtugaimid orainn féin) ar [an leathanach pobail][pobal].

### Nuashonrú agus Díshuiteáil

Nuair a bheidh Rust suiteáilte trí `rustup`, déantar nuashonrú go leagan nua-eisithe
éasca. Ó do bhlaosc, rith an script nuashonraithe seo a leanas:

```console
$ rustup update
```

Chun Rust agus `rustup` a dhíshuiteáil, rith an script díshuiteála seo a leanas ó do
sliogán:

```console
$ rustup self uninstall
```

### Doiciméadúchán Áitiúil

Cuimsíonn suiteáil Rust cóip áitiúil de na doiciméid mar sin freisin
gur féidir leat é a léamh as líne. Rith `rustup doc` chun an doiciméadú áitiúil a oscailt
i do bhrabhsálaí.

Am ar bith a sholáthraíonn an leabharlann chaighdeánach cineál nó feidhm agus ní bhíonn
cinnte cad a dhéanann sé nó conas é a úsáid, bain úsáid as an comhéadan ríomhchlárú feidhmchlár
(API) doiciméadú a fháil amach!

[otherinstall]: https://forge.rust-lang.org/infra/other-installation-methods.html
[shuiteáil]: https://www.rust-lang.org/tools/install
[msvc]: https://rust-lang.github.io/rustup/installation/windows-msvc.html
[pobal]: https://www.rust-lang.org/community
[uirlisí]: https://www.rust-lang.org/tools
