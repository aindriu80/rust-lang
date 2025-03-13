# Láimhseáil Earráide

Is fíoras saoil iad earráidí i mbogearraí, mar sin tá roinnt gnéithe ag Rust le haghaidh
láimhseáil cásanna ina dtéann rud éigin mícheart. I go leor cásanna, éilíonn Rust
tú a admháil go bhféadfadh earráid a bheith ann agus gníomh éigin a dhéanamh roimh do
tiomsóidh cód. Déanann an riachtanas seo do chlár níos láidre trína chinntiú
go bhfaighidh tú amach earráidí agus go láimhseálfaidh tú iad go cuí sula mbíonn
do chód imscartha chuig táirgeadh!

Déanann Rust earráidí a ghrúpáil i dhá mhórchatagóir: _aisghabhála_ agus _do-aisghabhála_
earráidí. I gcás earráide inghnóthaithe, mar earráid _file not found_, is mó a dhéanaimid
dócha gur mhaith leat ach an fhadhb a thuairisciú don úsáideoir agus an oibríocht a dhéanamh arís.
Is comharthaí de fhabhtanna iad earráidí do-aisghabhála i gcónaí, mar shampla ag iarraidh rochtain a
suíomh níos faide ná deireadh sraithe, agus mar sin ba mhaith linn stop a chur láithreach ar an
clár.

Ní dhéanann formhór na dteangacha idirdhealú idir an dá chineál seo earráidí agus láimhseálann siad
araon ar an mbealach céanna, ag baint úsáide as meicníochtaí mar eisceachtaí. Níl Rust ag
eisceachtaí. Ina áit sin, tá an cineál `Result <T, E>` aige le haghaidh earráidí inghnóthaithe agus
an macra `panic!` a stopann cur i gcrích nuair a thagann an clár trasna ar
earráid do-aisghabhála. Clúdaíonn an chaibidil seo glaoch ar `panic!` ar dtús agus ansin cainteanna
faoi ​​luachanna `Result<T, E>` a thabhairt ar ais. Ina theannta sin, déanfaimid iniúchadh
breithnithe agus cinneadh á dhéanamh ar cheart iarracht a dhéanamh teacht ar ais ó earráid nó stopadh
forghníomhú.