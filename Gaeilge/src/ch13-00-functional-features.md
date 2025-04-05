# Gnéithe Feidhmiúla Teanga: Iterators agus Dúnadh

Fuair ​​dearadh Rust inspioráid ó go leor teangacha atá ann cheana féin agus
teicnící, agus tionchar suntasach amháin is ea _ríomhchlárú feidhme_.
Cuimsíonn ríomhchlárú i stíl fheidhmiúil feidhmeanna a úsáid mar luachanna trí
iad a rith in argóintí, iad a thabhairt ar ais ó fheidhmeanna eile, iad a shannadh
chuig athróga le cur i gcrích níos déanaí, agus mar sin de.

Sa chaibidil seo, ní bheidh muid ag déanamh díospóireachta ar an gceist cad is ríomhchlárú feidhmiúil ann
nach bhfuil ach ina ionad sin pléifidh sé roinnt gnéithe de Rust atá cosúil leo
gnéithe i go leor teangacha ar a dtugtar go minic feidhmiúil.

Go sonrach, clúdóimid:

- _Closures_, tógáil atá cosúil le feidhm is féidir leat a stóráil in athróg
- _Iterators_, bealach chun sraith eilimintí a phróiseáil
- Conas dúnadh agus atrialtóirí a úsáid chun an tionscadal I/O i gCaibidil 12 a fheabhsú
- Feidhmíocht dúnta agus iterators (Foláireamh Spoiler: tá siad níos tapúla ná
 seans go gceapfá!)

Tá roinnt gnéithe Rust eile clúdaithe againn cheana féin, cosúil le meaitseáil patrún agus
enums, a bhfuil tionchar freisin ag an stíl fheidhmiúil. Toisc máistreacht
Is cuid thábhachtach de scríbhneoireacht idiomatic, tapa Rust é dúnta agus iterators
cód, tabharfaimid an chaibidil iomlán seo dóibh.# Functional Language Features: Iterators and Closures
