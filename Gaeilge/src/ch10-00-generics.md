# Cineálacha Cineálta, Tréithe, agus Saolta

Tá uirlisí ag gach teanga ríomhchláraithe chun an dúbailt a láimhseáil go héifeachtach
de choincheapa. I Rust, tá uirlis amháin dá leithéid _generics_: seastáin teibí do
cineálacha coincréite nó airíonna eile. Is féidir linn iompar generics nó
conas a bhaineann siad le cineálacha eile gan fios cad a bheidh ina n-áit
nuair a bheidh an cód á thiomsú agus á rith.

Is féidir le feidhmeanna paraiméadair de chineál éigin a ghlacadh, in ionad cineál coincréite
cosúil le `i32` nó `String`, ar an mbealach céanna a ghlacann siad paraiméadair le anaithnid
luachanna chun an cód céanna a rith ar illuachanna nithiúla. Go deimhin, tá muid cheana féin
úsáidtear generics i gCaibidil 6 le `Option<T>`, i gCaibidil 8 le `Vec<T>` agus
`HashMap<K, V>`, agus i gCaibidil 9 le `Result<T, E>`. Sa chaibidil seo, beidh tú
iniúchadh a dhéanamh ar conas do chineálacha, feidhmeanna agus modhanna féin a shainiú le generics!

Ar dtús déanfaimid athbhreithniú ar conas feidhm a bhaint as chun dúbailt cód a laghdú. Déanfaimid
ansin bain úsáid as an teicníc chéanna chun feidhm chineálach a dhéanamh as dhá fheidhm a
difriúil ach amháin i gcineálacha a bparaiméadar. Míneoimid freisin conas é a úsáid
cineálacha cineálacha i struchtúir agus sainmhínithe enum.

Ansin foghlaimeoidh tú conas _traits_ a úsáid chun iompar a shainiú ar bhealach cineálach. tu
is féidir tréithe a chomhcheangal le cineálacha cineálach chun srian a chur ar chineál cineálach glacadh leis
ach na cineálacha sin a bhfuil iompar ar leith acu, i gcomparáid le cineál ar bith.

Ar deireadh, pléifimid _lifetimes_: cineálacha cineálacha éagsúla a thugann an
faisnéis a thiomsú faoin gcaoi a mbaineann tagairtí lena chéile. Ceadaíonn saolré
go leor eolais a thabhairt don tiomsaitheoir faoi luachanna a fuarthas ar iasacht ionas gur féidir leis
a chinntiú go mbeidh teistiméireachtaí bailí i níos mó cásanna ná mar a d'fhéadfadh sé gan ár
cabhair.

## Dúbailt a Bhaint Trí Feidhm a Bhaint as

Ceadaíonn Generics dúinn cineálacha sonracha a athsholáthar le sealbhóir áit a léiríonn
cineálacha iomadúla chun dúbailt cód a bhaint. Sula tumadh isteach i gcomhréir generics,
Breathnaímid ar dtús ar conas dúbailt a bhaint ar bhealach nach mbaineann
cineálacha cineálacha trí fheidhm a bhaint a chuireann a
áitshealbhóir a léiríonn luachanna iolracha. Ansin cuirfimid an rud céanna i bhfeidhm
teicníc chun feidhm chineálach a bhaint as! Trí féachaint ar conas a aithint
cód dúblach is féidir leat a bhaint as feidhm, a thosóidh tú á aithint
cód dúblach is féidir a úsáid generics.

Cuirfimid tús leis an gclár gearr i Liostú 10-1 a aimsíonn an ceann is mó
uimhir i liosta.

<Listing number="10-1" file-name="src/main.rs" caption="Finding the largest number in a list of numbers">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-01/src/main.rs:here}}
```

</Listing>

Stórálaimid liosta slánuimhreacha san athróg `number_list` agus cuirimid tagairt
go dtí an chéad uimhir ar an liosta in athróg darb ainm `largest`. Déanaimid athrá ansin
trí na huimhreacha go léir sa liosta, agus má tá an uimhir reatha níos mó ná
an uimhir atá stóráilte in `largest`, cuirimid in ionad na tagartha san athróg sin.
Mar sin féin, má tá an líon reatha níos lú ná nó cothrom leis an líon is mó a fheictear
go dtí seo, ní athraíonn an athróg, agus bogann an cód ar aghaidh go dtí an chéad uimhir eile
sa liosta. Tar éis na huimhreacha go léir ar an liosta a mheas, ba cheart go mbeadh `largest`
tagairt a dhéanamh don líon is mó, atá sa chás seo 100.

Tá sé de chúram orainn anois an líon is mó a aimsiú in dhá liosta éagsúla de
uimhreacha. Chun é sin a dhéanamh, is féidir linn a roghnú an cód i Liostú 10-1 a dhúbailt agus a úsáid
an loighic chéanna ag dhá áit dhifriúla sa chlár, mar a léirítear i Liosta 10-2.

<Listing number="10-2" file-name="src/main.rs" caption="Code to find the largest number in *two* lists of numbers">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-02/src/main.rs}}
```

</Listing>

Cé go n-oibríonn an cód seo, bíonn dúbláil cód tedious agus seans maith go hearráidí. Táimid freisin
ní mór cuimhneamh ar an gcód a nuashonrú in áiteanna éagsúla nuair is mian linn athrú a dhéanamh
é.

Chun deireadh a chur leis an dúbailt seo, cruthóimid astarraingt trí a
feidhm a fheidhmíonn ar aon liosta slánuimhreacha a chuirtear isteach mar pharaiméadar. seo
réiteach a dhéanann ár gcód níos soiléire agus ligeann dúinn a chur in iúl an coincheap a aimsiú ar an
an líon is mó i liosta go hachomair.

I Liostú 10-3, bainimid an cód a aimsíonn an uimhir is mó in a
feidhm darb ainm `largest`. Ansin tugaimid an fheidhm chun an líon is mó a fháil
sa dá liosta ó Liosta 10-2. D'fhéadfaimis an fheidhm a úsáid ar aon cheann eile freisin
liosta de na luachanna `i32` a d'fhéadfadh a bheith againn sa todhchaí.

<Listing number="10-3" file-name="src/main.rs" caption="Abstracted code to find the largest number in two lists">

```rust
{{#rustdoc_include ../../listings/ch10-generic-types-traits-and-lifetimes/listing-10-03/src/main.rs:here}}
```

</Listing>

Tá paraiméadar ar a dtugtar `list` ag an bhfeidhm `largest`, a sheasann d'aon cheann
slis choincréite de luachanna `i32` a d'fhéadfaimis dul isteach san fheidhm. Mar thoradh air sin,
nuair a ghlaoimid an fheidhm, ritheann an cód ar na luachanna sonracha a rithimid
isteach.

Go hachomair, seo na céimeanna a ghlacamar chun an cód a athrú ó Liostú 10-2 go
Liostáil 10-3:

1. Cód dúblach a aithint.
1. Sliocht an cód dúblach isteach i gcorp na feidhme, agus sonraigh an
 ionchuir agus luachanna aischuir an chóid sin i síniú na feidhme.
1. Nuashonraigh an dá chás de chód dúblach chun an fheidhm a ghlaoch ina ionad.

Ansin, úsáidfimid na céimeanna céanna seo le cineálacha cineálacha chun dúbailt cód a laghdú. I
ar an mbealach céanna is féidir leis an gcomhlacht feidhme oibriú ar `list` teibí ina ionad sin
de luachanna sonracha, ceadaíonn generics cód oibriú ar chineálacha teibí.

Mar shampla, abair go raibh dhá fheidhm againn: ceann a aimsíonn an mhír is mó in a
slice de luachanna `i32` agus ceann a aimsíonn an mhír is mó i slice de `char`
luachanna. Conas a chuirfimid deireadh leis an dúbailt sin? Faighimis amach!