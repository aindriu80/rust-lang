## Feidhmíocht a Chomparáid: Lúb vs. Iterators

Chun a chinneadh cé acu lúb nó iterators a úsáid, ní mór duit fios a bheith agat cé acu
tá cur i bhfeidhm níos tapúla: an leagan den fheidhm `search` le sainráite
`for` lúb nó an leagan le iterators.

Reáchtáileamar tagarmharc trí ábhar iomlán _The Adventures of
Sherlock Holmes_ le Sir Arthur Conan Doyle isteach i `String` agus ag lorg an
focal _the_ san ábhar. Seo iad torthaí an tagarmhairc ar an
leagan de `search` ag baint úsáide as an lúb `for` agus an leagan ag baint úsáide as iterators:

```text
test bench_search_for  ... bench:  19,620,300 ns/iter (+/- 915,700)
test bench_search_iter ... bench:  19,234,900 ns/iter (+/- 657,200)
```

Tá feidhmíocht den chineál céanna ag an dá fheidhmiú! Ní mhíneoimid an
cód tagarmharcála anseo, toisc nach bhfuil an pointe a chruthú go bhfuil an dá leagan
comhionann ach chun tuiscint ghinearálta a fháil ar an gcaoi a bhfuil an dá fheidhmiú seo
i gcomparáid le feidhmíocht-ciallmhar.

Chun tagarmharc níos cuimsithí a fháil, ba cheart duit seiceáil ag baint úsáide as téacsanna éagsúla de
méideanna éagsúla mar an `contents`, focail éagsúla agus focail d'fhaid éagsúla
mar an `query`, agus gach cineál éagsúlachta eile. Is é an pointe seo:
iterators, cé gur astarraingt ardleibhéil, a thiomsú síos go dtí thart ar an
an cód céanna agus a bheadh ​​dá scríobhfá an cód leibhéal níos ísle tú féin. Tá iterators amháin
as astarraingtí _nialais-chostais_ Rust, rud a chiallaíonn úsáid as an astarraingt
ní fhorchuirtear aon am rite breise. Tá sé seo cosúil le conas Bjarne
Sainmhíníonn Stroustrup, dearthóir bunaidh agus feidhmitheoir C++
_zero-overhead_ in “Fondúireachtaí C++” (2012):

> Go ginearálta, cloíonn feidhmeanna C++ leis an bprionsabal náid forchostais: Cad atá tú
> ná húsáid, ní íocann tú as. Agus anuas air sin: An rud a úsáideann tú, ní fhéadfá lámh a chur air
> cód ar bith níos fearr.

Mar shampla eile, tógtar an cód seo a leanas ó dhíchódóir fuaime. Tá an
úsáideann algartam díchódaithe an oibríocht matamaitice tuar líneach chun
meastachán a dhéanamh ar luachanna na todhchaí bunaithe ar fheidhm líneach de na samplaí roimhe seo. seo
Úsáideann cód slabhra iterator chun roinnt matamaitice a dhéanamh ar thrí athróg i raon feidhme: a
slice de shonraí `buffer`, sraith de 12 `coefficients`, agus méid faoina
chun sonraí a aistriú in `qlp_shift`. Dhearbhaigh muid na hathróga laistigh den sampla seo
ach níor tugadh aon luachanna dóibh; cé nach bhfuil mórán brí leis an gcód seo
taobh amuigh dá chomhthéacs, is sampla gonta, fíor-dhomhain é fós den chaoi a bhfuil Rust
aistríonn smaointe ardleibhéil go cód ísealleibhéil.

```rust,ignore
let buffer: &mut [i32];
let coefficients: [i64; 12];
let qlp_shift: i16;

for i in 12..buffer.len() {
    let prediction = coefficients.iter()
                                 .zip(&buffer[i - 12..i])
                                 .map(|(&c, &s)| c * s as i64)
                                 .sum::<i64>() >> qlp_shift;
    let delta = buffer[i];
    buffer[i] = prediction as i32 + delta;
}
```

Chun luach `prediction` a ríomh, atriálann an cód seo trí gach ceann de na
12 luach i `coefficients` agus úsáidtear an modh `zip` chun an chomhéifeacht a phéireáil
luachanna leis na 12 luach roimhe seo sa `buffer`. Ansin, do gach péire, muid
iolrú na luachanna le chéile, suim na torthaí go léir, agus aistrigh na giotán sa
suimigh `qlp_shift` ar dheis.

Is minic a thugann ríomhanna in fheidhmchláir mar dhíchódóirí fuaime tosaíocht don fheidhmíocht
is airde. Anseo, tá iterator á chruthú againn, ag baint úsáide as dhá oiriúntóir, agus ansin
ag caitheamh an luacha. Cén cód tionóil a dhéanfadh an cód Rust seo a thiomsú dó? Bhuel,
ó thaobh na scríbhneoireachta seo de, tiomsaíonn sé síos go dtí an tionól céanna a scríobhfá de láimh.
Níl aon lúb ar chor ar bith a fhreagraíonn don atriall thar na luachanna i
`coefficients`: Tá a fhios ag Rust go bhfuil 12 atriall ann, mar sin "dírollaíonn sé" an
lúb. Is optamú é _Unrolling_ a bhainfidh an lastuas den lúb
cód rialaithe agus ina ionad sin gineann sé cód athchleachtach do gach atriall de
an lúb.

Faigheann gach comhéifeachtaí a stóráil i gcláir, rud a chiallaíonn rochtain a fháil ar an
luachanna an-tapa. Níl aon seiceálacha teorann ar an rochtain eagair ag am rite.
Déanann na huasmhéaduithe seo go léir a bhfuil Rust in ann a chur i bhfeidhm an cód a eascraíonn as
thar a bheith éifeachtach. Anois go bhfuil sé seo ar eolas agat, is féidir leat iterators agus dúnta a úsáid
gan eagla! Déanann siad cosúil go bhfuil cód ag leibhéal níos airde ach ní fhorchuireann siad a
pionós feidhmíochta ritime as é sin a dhéanamh.

## Achoimre

Is gnéithe Rust iad dúnta agus iterators spreagtha ag ríomhchlárú feidhmiúil
smaointe teanga. Cuireann siad le cumas Rust a chur in iúl go soiléir
smaointe ardleibhéil ar fheidhmíocht ísealleibhéil. Feidhmeanna dúnta agus
is amhlaidh nach gcuirtear isteach ar fheidhmíocht am rite. Tá sé seo mar chuid de
Tá sé mar sprioc ag Rust a dhícheall a dhéanamh astarraingtí gan costas a sholáthar.

Anois go bhfuil sainléiriú ár dtionscadal I/O feabhsaithe againn, féachaimis
roinnt gnéithe níos mó de `cargo` a chabhróidh linn an tionscadal a roinnt leis an
domhan.