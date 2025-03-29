## Ag Obair le hAthróga Comhshaoil

Feabhsóimid `minigrep` trí ghné bhreise a chur leis: rogha le haghaidh
cuardach cás-íogair ar féidir leis an úsáideoir a chur ar siúl trí thimpeallacht
athróg. D'fhéadfaimis an ghné seo a dhéanamh mar rogha na n-orduithe agus é sin a éileamh
cuireann úsáideoirí isteach é gach uair is mian leo é a chur i bhfeidhm, ach ina ionad sin é a dhéanamh
athróg timpeallachta, tugaimid deis dár n-úsáideoirí an athróg timpeallachta a shocrú uair amháin
agus bíodh a gcuardach uile neamhíogair sa seisiún teirminéil sin.

### Triail Theip a Scríobh don Fheidhm `search` Cás-íogair

Ar dtús cuirimid feidhm nua `search_case_insensitive` isteach ar a dtabharfar nuair
tá luach ag an athróg timpeallachta. Leanfaimid orainn ag leanúint leis an bpróiseas TDD,
mar sin is é an chéad chéim arís triail theipthe a scríobh. Cuirfimid triail nua leis
an fheidhm nua `search_case_insensitive` agus athainmnigh ár sean-triail ó
`one_result` go `case_sensitive` chun na difríochtaí idir an dá rud a shoiléiriú
tástálacha, mar a thaispeántar i Liostú 12-20.

<Listing number="12-20" file-name="src/lib.rs" caption="Adding a new failing test for the case-insensitive function we’re about to add">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-20/src/lib.rs:here}}
```

</Listing>

Tabhair faoi deara go bhfuil `contents` na sean-thástála curtha in eagar againn freisin. Tá líne nua curtha leis againn
leis an téacs `"Duct tape."` ag baint úsáide as ceannlitir _D_ nár cheart a bheith ag teacht leis an gceist
`"duct"` nuair a bhíonn muid ag cuardach ar bhealach cás-íogair. Athrú ar an tástáil d'aois
ar an mbealach seo cabhraíonn sé lena chinntiú nach mbrisimid an cás-íogair trí thimpiste
feidhmiúlacht chuardaigh atá curtha i bhfeidhm againn cheana féin. Ba cheart go n-éireodh leis an tástáil seo anois
agus ba chóir go leanfadh sé ar aghaidh agus muid ag obair ar an gcuardach cás-íogair.

Úsáideann an tástáil nua don chuardach cás-_insensitive_ `"rUsT"` mar cheist. I
an fheidhm `search_case_insensitive` atáimid ar tí cur leis, an cheist `"rUsT"`
Ba chóir go mbeadh an líne ina bhfuil `"Rust:"` le príomhchathair _R_ agus an líne a mheaitseáil
line `"Trust me."` cé go bhfuil cásáil éagsúil ag an mbeirt ón gceist. seo
Is é ár dtástáil theip, agus ní theipfidh orainn é a thiomsú toisc nach bhfuil sainithe againn fós
an fheidhm `search_case_insensitive`. Thig leat creatlach a chur leis
cur i bhfeidhm a thugann veicteoir folamh ar ais i gcónaí, cosúil leis an mbealach a rinne muid
don fheidhm `search` i Liostú 12-16 chun an tástáil a thiomsú agus a theipeann a fheiceáil.

### Feidhm `search_case_insensitive` á cur i bhfeidhm

Beidh an fheidhm `search_case_insensitive`, a thaispeántar i Liostú 12-21, beagnach
mar an gcéanna leis an bhfeidhm `search`. Is é an t-aon difríocht ná go ndéanfaimid cás íochtair
an `query` agus gach `line` ionas gur cuma cad é cás na n-argóintí ionchuir,
beidh siad mar an gcéanna nuair a dhéanaimid seiceáil an bhfuil an cheist sa líne.

<Listing number="12-21" file-name="src/lib.rs" caption="Defining the `search_case_insensitive` function to lowercase the query and the line before comparing them">

```rust,noplayground
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-21/src/lib.rs:here}}
```

</Listing>

Ar dtús déanaimid an sreang `query` a íoslaghdú agus é a stóráil in athróg nua leis an
ainm céanna, ag scáthú an bhunaidh. Glaoitear `go_lowercase` ar an gceist
riachtanach ionas gur cuma cé acu an bhfuil ceist an úsáideora `"rust"`, `"RUST"`,
`"Rust"`, nó `"rUsT"`, déileálfaimid leis an gceist amhail is dá mba `"rust"` é agus beidh
neamhíogair don chás. Cé go láimhseálfaidh `to_lowercase` Unicode bhunúsach, beidh sé
ní bheidh sé 100% cruinn. Dá mbeimis ag scríobh fíor-iarratas, ba mhaith linn a
beagán níos mó oibre anseo, ach baineann an chuid seo le hathróga timpeallachta, nach bhfuil
Unicode, mar sin fágfaimid anseo é.

Tabhair faoi deara gur `String` é `query` anois seachas sreangán mar gheall ar ghlaoch
cruthaíonn `to_lowercase` sonraí nua seachas tagairt a dhéanamh do shonraí atá ann cheana féin. Abair an
Is é `"rUsT"` an cheist, mar shampla: níl cás íochtair sa téad sliseog sin
`u` nó `t` le húsáid againn, mar sin ní mór dúinn `String` nua a leithdháileadh ina bhfuil
`"rust"`. Nuair a thugaimid `query` mar argóint don mhodh `contains` anois, déanaimid
gá ampersand a chur leis toisc go bhfuil síniú `tá` sainithe le glacadh
slisne teaghrán.

Ansin, cuirimid glao chuig `to_lowercase` ar gach `line` chun gach cás a laghdú
carachtair. Anois go bhfuil `line` agus `query` tiontaithe againn go cás íochtair, déanfaimid
aimsigh meaitseanna is cuma cad é cás an fhiosrúcháin.

Feicfimid an éiríonn leis an gcur i bhfeidhm seo na tástálacha:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-21/output.txt}}
```

Go hiontach! Rith siad. Anois, cuirimis glaoch ar an bhfeidhm nua `search_case_insensitive`
ón bhfeidhm `run`. Ar dtús cuirfimid rogha cumraíochta leis an `Config`
déan iarracht aistriú idir cuardach cás-íogair agus cás-íogair. Ag cur
cruthóidh an réimse seo earráidí tiomsaithe toisc nach bhfuilimid ag tosú an réimse seo
áit ar bith go fóill:

<span class="filename">Filename: src/lib.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-22/src/lib.rs:here}}
```

Chuireamar an réimse `ignore_case` isteach a bhfuil Boole aige. Ansin, ní mór dúinn an `run`
feidhm chun luach an réimse `ignore_case` a sheiceáil agus é sin a úsáid chun cinneadh a dhéanamh
cibé ar cheart an fheidhm `search` nó an `search_case_insensitive` a ghlaoch
fheidhm, mar a thaispeántar i Liostú 12-22. Ní bheidh sé seo le chéile go fóill.

<Listing number="12-22" file-name="src/lib.rs" caption="Calling either `search` or `search_case_insensitive` based on the value in `config.ignore_case`">

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-22/src/lib.rs:there}}
```

</Listing>

Ar deireadh, ní mór dúinn a sheiceáil le haghaidh an athróg timpeallachta. Na feidhmeanna le haghaidh
tá oibriú le hathróga timpeallachta sa mhodúl `env` sa chaighdeán
leabharlann, mar sin tugaimid an modúl sin isteach sa scóip ag barr _src/lib.rs_. Ansin
úsáidfimid an fheidhm `var` ón modúl `env` le seiceáil an bhfuil aon luach ann
socraithe d'athróg timpeallachta darb ainm `IGNORE_CASE`, mar a thaispeántar i
Liostáil 12-23.

<Listing number="12-23" file-name="src/lib.rs" caption="Checking for any value in an environment variable named `IGNORE_CASE`">

```rust,noplayground
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-23/src/lib.rs:here}}
```

</Listing>

Anseo, cruthaímid athróg nua, `ignore_case`. Chun a luach a shocrú, tugaimid an
feidhm `env::var` agus cuir ainm na timpeallachta `IGNORE_CASE` air
athróg. Tugann an fheidhm `env::var` ar ais a bheidh mar an
malairt `Ok` rathúil ina bhfuil luach na hathróige timpeallachta más rud é
socraítear athróg an chomhshaoil ​​ar aon luach. Tabharfaidh sé ar ais an leagan `Err`
mura bhfuil an athróg timpeallachta socraithe.

Táimid ag baint úsáide as an modh `is_ok` ar an `Result` le seiceáil an bhfuil an timpeallacht
Tá athróg socraithe, rud a chiallaíonn gur cheart don chlár cuardach cás-íogair a dhéanamh.
Mura bhfuil an athróg timpeallachta `IGNORE_CASE` socraithe mar rud ar bith, beidh `is_ok`
fill `false` agus déanfaidh an clár cuardach cás-íogair. Ní dhéanaimid
aire a thabhairt do _luach_ na hathróige timpeallachta, díreach cibé an bhfuil sé socraithe nó
gan a bheith socraithe, mar sin táimid ag seiceáil `is_ok` seachas `unwrap`, `expect`, nó aon cheann a úsáid
de na modhanna eile atá feicthe againn ar `Result`.

Tugaimid an luach san athróg `ignore_case` go dtí an t- shampla `Config` mar sin de
Is féidir le feidhm `run` an luach sin a léamh agus cinneadh a dhéanamh ar cheart glaoch
`search_case_insensitive` nó `search`, mar a chuireamar i bhfeidhm i Liostú 12-22.

Déanaimis iarracht é! Ar dtús rithfidh muid ár gclár gan an timpeallacht
tacar athróg agus leis an gceist `to`, ba cheart go mbeadh sé ag teacht le haon líne atá ann
an focal _to_ i ngach cás íochtair:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-23/output.txt}}
```

Is cosúil go n-oibríonn go fóill! Anois, déanaimis an clár a reáchtáil le sraith `IGNORE_CASE`
go `1` ach leis an gceist chéanna _to_:

```console
$ IGNORE_CASE=1 cargo run -- to poem.txt
```

Má tá PowerShell á úsáid agat, beidh ort an athróg timpeallachta a shocrú agus
rith an clár mar orduithe ar leith:

```console
PS> $Env:IGNORE_CASE=1; cargo run -- to poem.txt
```

Fágfaidh sé seo go seasfaidh `IGNORE_CASE` ar feadh an chuid eile de do sheisiún sliogán.
Is féidir é a dhíshuiteáil leis an cmdlet `Remove-Item`:

```console
PS> Remove-Item Env:IGNORE_CASE
```

Ba cheart dúinn línte a fháil ina bhfuil _to_ a bhféadfadh litreacha móra a bheith orthu:

<!-- manual-regeneration
cd listings/ch12-an-io-project/listing-12-23
IGNORE_CASE=1 cargo run -- to poem.txt
can't extract because of the environment variable
-->

```console
Are you nobody, too?
How dreary to be somebody!
To tell your name the livelong day
To an admiring bog!
```

Ar fheabhas, fuaireamar línte freisin ina raibh _To_! Is féidir lenár gclár `minigrep` a dhéanamh anois
cuardach cás-íogair arna rialú ag athróg timpeallachta. Anois tá a fhios agat
conas na roghanna atá leagtha síos a bhainistiú trí úsáid a bhaint as argóintí na n-orduithe nó as timpeallacht
athróga.

Ceadaíonn roinnt clár argóintí _agus_ athróga timpeallachta mar an gcéanna
cumraíocht. Sna cásanna sin, cinneann na cláir a thógann ceann amháin nó an ceann eile
tosaíocht. Le haghaidh cleachtaidh eile leat féin, déan iarracht íogaireacht cáis a rialú
trí argóint ceannlíne nó trí athróg timpeallachta. Déan cinneadh
cé acu ar cheart argóint na n-orduithe nó an athróg timpeallachta a ghlacadh
tosaíocht má reáchtálfar an clár le sraith amháin go cásíogair agus sraith amháin go
neamhaird a dhéanamh ar chás.

Tá i bhfad níos mó gnéithe úsáideacha le plé sa mhodúl `std::env`
athróga timpeallachta: seiceáil a dhoiciméadú chun a fháil amach cad atá ar fáil.