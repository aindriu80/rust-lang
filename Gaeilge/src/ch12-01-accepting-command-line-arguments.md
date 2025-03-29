## Ag glacadh le Argóintí Líne Ordú

Cruthaímid tionscadal nua le, mar i gcónaí, `cargo new`. Cuirfimid glaoch ar ár dtionscadal
`minigrep` chun é a idirdhealú ón uirlis `grep` a d'fhéadfadh a bheith agat cheana féin
ar do chóras.

```console
$ cargo new minigrep
     Created binary (application) `minigrep` project
$ cd minigrep
```

Is é an chéad tasc a thabhairt ar `minigrep` glacadh lena dhá argóint na n-orduithe: an
cosán comhaid agus teaghrán le cuardach a dhéanamh air. Is é sin, ba mhaith linn a bheith in ann ár gcuid
clár le `cargo run`, dhá thángthas ar na hargóintí seo a leanas a chur in iúl
dár gclár seachas don `cargo`, teaghrán le cuardach a dhéanamh air, agus cosán chuige
comhad le cuardach a dhéanamh ann, mar seo:

```console
$ cargo run -- searchstring example-filename.txt
```

Faoi láthair, ní féidir leis an gclár a ghineann `cargo new` argóintí a phróiseáil
tabhair. Is féidir le roinnt leabharlanna atá ann cheana féin ar [crates.io](https://crates.io/) cabhrú
le clár a scríobh a ghlacann le hargóintí na n-orduithe, ach toisc go bhfuil tú
ach an coincheap seo a fhoghlaim, cuirimis an cumas seo i bhfeidhm sinn féin.

### Léamh na Luachanna Argóna

Le cur ar chumas `minigrep` luachanna na n-argóintí ordú a chuirimid ar aghaidh chucu a léamh
é, beidh an fheidhm `std::env::args` a sholáthraítear i gcaighdeán Rust de dhíth orainn
leabharlann. Tugann an fheidhm seo atriarthóir ar na hargóintí ordú a ritheadh ​​ar ais
go `minigrep`. Clúdóimid atrialltóirí go hiomlán i [Caibidil 13][ch13]<!-- déan neamhaird
-->. Faoi láthair, ní gá duit ach fios a bheith agat ar dhá shonra faoi iterators: iterators
sraith luachanna a tháirgeadh, agus is féidir linn an modh `collect` a ghlaoch ar iterator
chun é a iompú ina bhailiúchán, mar veicteoir, ina bhfuil na heilimintí go léir
táirgeann an t-iterator.

Ligeann an cód i Liostú 12-1 do do chlár `minigrep` ordú ar bith a léamh
argóintí líne a cuireadh ar aghaidh chuige, agus ansin na luachanna a bhailiú i veicteoir.

<Listing number="12-1" file-name="src/main.rs" caption="Collecting the command line arguments into a vector and printing them">

```rust
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-01/src/main.rs}}
```

</Listing>

Ar dtús cuirimid an modúl `std::env` isteach sa scóip le ráiteas `use` mar sin déanaimid
is féidir a fheidhm `args` a úsáid. Tabhair faoi deara gurb é an fheidhm `std::env::args`
neadaithe in dhá leibhéal de mhodúil. Mar a phléamar i [Caibidil
7][ch7-idiomatic-use] <!-- neamhaird a dhéanamh ar -->, i gcásanna ina bhfuil an fheidhm inmhianaithe
neadaithe i níos mó ná modúl amháin, roghnaigh muid an modúl tuismitheora a thabhairt isteach
scóip seachas an fheidhm. Trí é sin a dhéanamh, is féidir linn feidhmeanna eile a úsáid go héasca
ó `std::env`. Níl sé chomh débhríoch freisin ná `use std::env::args` agus
ansin an fheidhm a ghlaoch le `args`, mar is furasta `args` a bheith i gceist
cearr le feidhm atá sainmhínithe sa mhodúl reatha.

> ### Feidhm `args` agus Unicode Neamhbhailí
>
> Tabhair faoi deara go rachaidh `std::env::args` i scaoll má tá argóint neamhbhailí ann
> Unicode. Más gá do do chlár glacadh le hargóintí ina bhfuil neamhbhailí
> Unicode, bain úsáid as `std::env::args_os` ina ionad sin. Tugann an fheidhm sin aterator ar ais
> a tháirgeann luachanna `OsString` in ionad luachanna `String`. Roghnaíomar
> úsáid `std::env::args` anseo le haghaidh simplíochta mar go bhfuil luachanna `OsString` difriúil in aghaidh na
> ardán agus tá siad níos casta oibriú leo ná luachanna `String`.

Ar an gcéad líne de `main`, tugaimid `env::args`, agus úsáidimid láithreach
`collect` chun an t-iterator a iompú ina veicteoir ina bhfuil na luachanna go léir a tháirgtear
ag an iterator. Is féidir linn an fheidhm `collect` a úsáid chun go leor cineálacha de a chruthú
bailiúcháin, mar sin déanaimid anótáil go sainráite ar an gcineál `args` lena shonrú go bhfuilimid
ag iarraidh veicteoir teaghráin. Cé gur annamh a chaithfidh tú cineálacha a anótáil i
Meirge, is feidhm amháin é `collect` is minic a chaithfidh tú anótáil a dhéanamh uirthi toisc go bhfuil Rust
níl sé in ann an cineál bailiúcháin atá uait a thuiscint.

Ar deireadh, priontálaimid an veicteoir ag baint úsáide as an macra dífhabhtaithe. Déanaimis iarracht an cód a rith
ar dtús gan argóintí ar bith agus ansin le dhá argóint:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-01/output.txt}}
```

```console
{{#include ../../listings/ch12-an-io-project/output-only-01-with-args/output.txt}}
```

Tabhair faoi deara gurb é `"target/debug/minigrep"` an chéad luach sa veicteoir, a
is ainm dár dénártha. Meaitseálann sé seo iompar an liosta argóintí i
C, cláir ligean ar cíos úsáid a bhaint as an t-ainm a bhí á agairt agus iad i gcrích.
Is minic a bhíonn sé áisiúil rochtain a fháil ar ainm an chláir ar eagla go dteastaíonn uait
é a phriontáil i dteachtaireachtaí nó iompar an chláir a athrú bunaithe ar an méid
Baineadh úsáid as ailias na líne ordaithe chun an clár a agairt. Ach chun críocha seo
chaibidil, déanfaimid neamhaird de agus ní shábhálfaimid ach an dá argóint a theastaíonn uainn.

### Luachanna Argóint a Shábháil in Athróga

Tá an clár in ann rochtain a fháil ar na luachanna atá sonraithe mar líne ordaithe faoi láthair
argóintí. Anois caithfimid luachanna an dá argóint a shábháil in athróga mar sin de
is féidir linn na luachanna a úsáid ar fud an chuid eile den chlár. Déanaimid é sin i Liostú
12-2.

<Listing number="12-2" file-name="src/main.rs" caption="Creating variables to hold the query argument and file path argument">

```rust,should_panic,noplayground
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-02/src/main.rs}}
```

</Listing>

Mar a chonaic muid nuair a phriontáileamar an veicteoir, is é ainm an chláir an chéad cheann
luach sa veicteoir ag `args[0]`, mar sin táimid ag tosú argóintí ag innéacs 1. Tá an
Is é an chéad argóint a thógann `minigrep` an teaghrán atá á lorg againn, mar sin cuirimid a
tagairt don chéad argóint san athróg `query`. An dara argóint
Beidh an cosán comhad, mar sin chuir muid tagairt don dara argóint sa
athróg `file_path`.

Déanaimid luachanna na n-athróg seo a phriontáil go sealadach chun a chruthú go bhfuil an cód
ag obair mar atá beartaithe againn. Déanaimis an clár seo a rith arís leis na hargóintí `test`
agus `sample.txt`:

```console
{{#include ../../listings/ch12-an-io-project/listing-12-02/output.txt}}
```

Go hiontach, tá an clár ag obair! Is iad luachanna na n-argóintí a theastaíonn uainn
shábháil isteach na hathróga cearta. Níos déanaí cuirfimid roinnt láimhseáil earráide leis chun déileáil leis
le cásanna earráideacha féideartha áirithe, mar shampla nuair a sholáthraíonn an t-úsáideoir uimh
argóintí; faoi ​​láthair, déanfaimid neamhaird den scéal sin agus oibreoimid ar léamh comhaid a chur leis
cumais ina ionad.

[ch13]: ch13-00-functional-features.html
[ch7-idiomatic-use]: ch07-04-bringing-paths-into-scope-with-the-use-keyword.html#creating-idiomatic-use-paths