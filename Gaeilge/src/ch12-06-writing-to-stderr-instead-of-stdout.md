## Teachtaireachtaí Earráide á Scríobh go Earráid Chaighdeánach In ionad Aschur Caighdeánach

Faoi láthair, táimid ag scríobh ár n-aschur go léir chuig an teirminéal ag baint úsáide as an
`println!` macra. I bhformhór na gcríochfort, tá dhá chineál aschuir: _standard
aschur_ (`stdout`) le haghaidh faisnéise ginearálta agus _earráid chaighdeánach_ (`stderr`) le haghaidh
teachtaireachtaí earráide. Cuireann an t-idirdhealú seo ar chumas úsáideoirí rogha a dhéanamh chun an
aschur rathúil clár go comhad ach fós teachtaireachtaí earráide a phriontáil chuig an
scáileán.

Níl an macra `println!` in ann priontáil ach go dtí aschur caighdeánach, mar sin ní mór dúinn
rud éigin eile a úsáid le priontáil go hearráid chaighdeánach.

### Ag Seiceáil Cá bhfuil Earráidí Scríofa

Ar dtús déanaimis breathnú ar an gcaoi a bhfuil an t-ábhar atá clóite ag `minigrep` á phriontáil faoi láthair
scríofa chuig aschur caighdeánach, lena n-áirítear aon teachtaireachtaí earráide ar mhaith linn scríobh chucu
earráid chaighdeánach ina ionad sin. Déanfaimid é sin tríd an sruth caighdeánach aschuir a atreorú
chuig comhad agus é ina chúis le hearráid d'aon ghnó. Ní dhéanfaimid an caighdeán a atreorú
sruth earráide, mar sin beidh aon ábhar a seoladh chuig earráid chaighdeánach ar aghaidh ag taispeáint ar
an scáileán.

Táthar ag súil go seolfaidh cláir líne ordaithe teachtaireachtaí earráide chuig an earráid chaighdeánach
sruth ionas gur féidir linn fós teachtaireachtaí earráide a fheiceáil ar an scáileán fiú má atreoraíonn muid an
sruth caighdeánach aschuir chuig comhad. Níl ár gclár múinte faoi láthair:
táimid ar tí a fheiceáil go sábhálann sé aschur na teachtaireachta earráide chuig comhad ina ionad sin!

Leis an iompar seo a léiriú, rithfidh muid an clár le `>` agus cosán an chomhaid,
_output.txt_, ar mhaith linn an sruth caighdeánach aschuir a atreorú chuige. Ní dhéanfaimid
pas a fháil ar argóintí ar bith, ar cheart dóibh earráid a chruthú:

```console
$ cargo run > output.txt
```

Insíonn an chomhréir `>` don bhlaosc ábhar an aschuir chaighdeánaigh a scríobh chuige
_output.txt_ in ionad an scáileáin. Ní fhacamar an teachtaireacht earráide a bhí againn
ag súil clóite ar an scáileán, mar sin a chiallaíonn go gcaithfidh sé a bheith dar críoch suas sa
comhad. Seo a bhfuil i _output.txt_:

```text
Problem parsing arguments: not enough arguments
```

Sea, tá ár dteachtaireacht earráide á phriontáil go dtí an t-aschur caighdeánach. Tá sé i bhfad níos mó
úsáideach chun teachtaireachtaí earráide mar seo a phriontáil go hearráid chaighdeánach amháin
críochnaíonn sonraí ó rith rathúil suas sa chomhad. Athróimid é sin.

### Earráidí Priontála go Earráid Chaighdeánach

Úsáidfimid an cód i Liostú 12-24 chun an chaoi a phriontáiltear teachtaireachtaí earráide a athrú.
Mar gheall ar an refactoring rinne muid níos luaithe sa chaibidil seo, go léir an cód go
tá teachtaireachtaí earráide priontaí in aon fheidhm amháin, `main`. Soláthraíonn an leabharlann caighdeánach
an macra `eprintln!` a phriontálann go dtí an sruth caighdeánach earráide, mar sin déanaimis athrú
an dá áit a raibh muid ag glaoch `println!` chun earráidí a phriontáil chun `eprintln!` a úsáid
ina ionad.

<Listing number="12-24" file-name="src/main.rs" caption="Writing error messages to standard error instead of standard output using `eprintln!`">

```rust,ignore
{{#rustdoc_include ../../listings/ch12-an-io-project/listing-12-24/src/main.rs:here}}
```

</Listing>

Déanaimis an clár a rith arís ar an mbealach céanna, gan argóintí agus
aschur caighdeánach á atreorú le `>`:

```console
$ cargo run > output.txt
Problem parsing arguments: not enough arguments
```

Anois feicimid an earráid ar an scáileán agus níl aon rud ag _output.txt_, is é sin an
iompar a mbeimid ag súil leis ó chláir na n-orduithe.

Rithfimid an clár arís le hargóintí nach n-eascraíonn earráid ach atá fós
atreorú aschur caighdeánach chuig comhad, mar sin:

```console
$ cargo run -- to poem.txt > output.txt
```

Ní fheicfimid aon aschur chuig an teirminéal, agus beidh ár gcuid _output.txt_
torthaí:

<span class="filename">Ainm comhaid: output.txt</span>

```text
Are you nobody, too?
How dreary to be somebody!
```

Léiríonn sé seo go bhfuil aschur caighdeánach á úsáid againn anois le haghaidh aschur rathúil
agus earráid chaighdeánach maidir le haschur earráide de réir mar is cuí.

## Achoimre

Rinne an chaibidil seo achoimre ar chuid de na mórchoincheapa atá foghlamtha agat go dtí seo agus
clúdaithe conas oibríochtaí coitianta I/O a dhéanamh i Rust. Trí úsáid a bhaint as líne ordaithe
argóintí, comhaid, athróga timpeallachta, agus an macra `eprintln!` le haghaidh priontála
earráidí, tá tú réidh anois feidhmchláir orduithe a scríobh. In éineacht le
na coincheapa i gcaibidlí roimhe seo, beidh do chód a bheith eagraithe go maith, sonraí a stóráil
go héifeachtach sna struchtúir sonraí cuí, earráidí a láimhseáil go deas, agus a bheith
dea-thástáil.

Ansin, déanfaimid iniúchadh ar roinnt gnéithe Rust a raibh tionchar ag feidhmiúil orthu
teangacha: dúnta agus iterators.