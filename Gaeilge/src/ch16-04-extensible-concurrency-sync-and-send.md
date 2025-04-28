## Comhthráthacht Inleathnaithe leis na Tréithe `Sync` agus `Send`

Is suimiúil go bhfuil _an-bheagán_ gnéithe comhthráthachta ag an teanga Rust. Tá beagnach
gach
gné comhthráthachta a phléamar go dtí seo sa chaibidil seo
mar chuid den leabharlann chaighdeánach, ní den teanga. Níl do roghanna maidir le láimhseáil
comthráthacht teoranta don teanga ná don leabharlann chaighdeánach; is féidir leat
do ghnéithe comhthráthachta féin a scríobh nó iad siúd a scríobh daoine eile a úsáid.

Mar sin féin, tá dhá choincheap comhthráthachta leabaithe sa teanga: na
tréithe `std::marker` `Sync` agus `Send`.

### Ceadú Aistriú Úinéireachta Idir Snáitheanna le `Send`

Léiríonn an tréith marcóra `Send` gur féidir úinéireacht luachanna den chineál
a chuireann `Send` i bhfeidhm a aistriú idir snáitheanna. Is beagnach gach cineál Rust é `Send`, ach tá roinnt eisceachtaí ann, lena n-áirítear `Rc<T>`: ní féidir é seo a bheith
`Send` mar má chlónálann tú luach `Rc<T>` agus má dhéanann tú iarracht úinéireacht an chlóin a aistriú
go snáithe eile, d'fhéadfadh an dá shnáithe an comhaireamh tagartha a nuashonrú
ag an am céanna. Ar an gcúis seo, cuirtear `Rc<T>` i bhfeidhm lena úsáid i
gcásanna aon-snáithe nach mian leat an pionós feidhmíochta sábháilte snáithe a íoc.

Dá bhrí sin, cinntíonn córas cineálacha agus teorainneacha tréithe Rust nach féidir leat
luach `Rc<T>` a sheoladh de thaisme trasna snáitheanna go neamhshábháilte. Nuair a rinneamar iarracht
é seo a dhéanamh i Liostáil 16-14, fuair muid an earráid `the trait Send is not implemented for
Rc<Mutex<i32>>`. Nuair a d'athraíomar go `Arc<T>`, arb é `Send` é, tiomsaíodh an cód.

Aon chineál atá comhdhéanta go hiomlán de chineálacha `Send`, marcáiltear go huathoibríoch mar `Send` chomh maith. Is `Send` beagnach gach cineál primitive, seachas pointeoirí amha, a phléifimid i gCaibidil 20.

### Ceadú Rochtain ó Il-Shnáitheanna le `Sync`

Léiríonn an tréith marcóra `Sync` go bhfuil sé sábháilte don chineál a chuireann `Sync` i bhfeidhm tagairt a dhéanamh dó ó il-shnáitheanna. I bhfocail eile, is `Sync` aon chineál `T` má tá `&T` (tagairt neamh-inathraithe do `T`) ina `Send`, rud a chiallaíonn gur féidir an tagairt a sheoladh go sábháilte chuig snáithe eile. Cosúil le `Send`, is `Sync` cineálacha primitive, agus is `Sync` cineálacha atá comhdhéanta go hiomlán de chineálacha atá ina `Sync` freisin.

Ní `Sync` an pointeoir cliste `Rc<T>` ar na cúiseanna céanna nach
`Send` é. Ní `Sync` an cineál `RefCell<T>` (a labhair muid faoi i gCaibidil 15) agus an
teaghlach de chineálacha gaolmhara `Cell<T>`. Níl cur i bhfeidhm iasachta
ag seiceáil go ndéanann `RefCell<T>` ag am rith sábháilte ó thaobh snáithe de. Is é `Sync` an pointeoir cliste
`Mutex<T>` agus is féidir é a úsáid chun rochtain a roinnt le snáitheanna
il mar a chonaic tú sa chuid ["`Mutex<T>` a roinnt idir snáitheanna iomadúla"][sharing-a-mutext-between-multiple-threads]<!-- ignore -->.

### Tá `Send` agus `Sync` a Chur i bhFeidhm de Láimh Neamhshábháilte

Toisc go bhfuil cineálacha atá comhdhéanta de thréithe `Send` agus `Sync` go huathoibríoch
freisin `Send` agus `Sync`, ní gá dúinn na tréithe sin a chur i bhfeidhm de láimh. Mar
thréithe marcóra, níl aon mhodhanna acu fiú le cur i bhfeidhm. Tá siad
úsáideach chun neamhathraitheach a bhaineann le comhthráthacht a fhorfheidhmiú.

Bíonn cód Rust neamhshábháilte á chur i bhfeidhm i gceist le cur i bhfeidhm na dtréithe seo de láimh.

Labhróimid faoi chód Rust neamhshábháilte a úsáid i gCaibidil 20; faoi ​​láthair, is é an fhaisnéis thábhachtach ná go n-éilíonn tógáil cineálacha comhthráthacha nua nach bhfuil comhdhéanta de chodanna `Send` agus
`Sync` machnamh cúramach chun na ráthaíochtaí sábháilteachta a choinneáil. Tá tuilleadh eolais faoi na ráthaíochtaí seo agus conas iad a choinneáil sa [“The
Rustonomicon”][nomicon].

## Achoimre

Ní hé seo an uair dheireanach a fheicfidh tú comhthráthacht sa leabhar seo: díríonn an chéad chaibidil eile ar fad ar chláreagrú neamhshioncrónach, agus úsáidfidh an tionscadal i gCaibidil 21 na
coincheapa sa chaibidil seo i gcás níos réadúla ná na samplaí níos lú
a phléitear anseo.

Mar a luadh cheana, toisc nach bhfuil mórán den chaoi a láimhseálann Rust comhthráthacht mar chuid den teanga, cuirtear go leor réitigh chomhthráthachta i bhfeidhm mar chliathbhoscaí.
Forbraíonn siad seo níos tapúla ná an leabharlann chaighdeánach, mar sin bí cinnte cuardach a dhéanamh ar líne le haghaidh na gcliathbhoscaí reatha, úrscothacha le húsáid i gcásanna il-shnáithithe.

Soláthraíonn leabharlann chaighdeánach Rust bealaí le haghaidh teachtaireachtaí a rith agus cineálacha pointeora cliste, amhail `Mutex<T>` agus `Arc<T>`, atá sábháilte le húsáid i gcomhthéacsanna comhthráthacha. Cinntíonn an córas cineálacha agus an seiceálaí iasachta nach mbeidh rásaí sonraí ná tagairtí neamhbhailí sa chód a úsáideann na réitigh seo.
Nuair a gheobhaidh tú do chód le tiomsú, is féidir leat a bheith cinnte go rithfidh sé go sona sásta ar ilshnáitheanna gan na cineálacha fabhtanna atá deacair a rianú atá coitianta i dteangacha eile. Ní coincheap le bheith eaglach roimhe a thuilleadh é cláir chomhthráthacha:
téigh ar aghaidh agus déan do chláir chomhthráthacha, gan eagla!

[sharing-a-mutext-between-multiple-threads]: ch16-03-shared-state.html#sharing-a-mutext-between-multiple-threads
[nomicon]: ../nomicon/index.html