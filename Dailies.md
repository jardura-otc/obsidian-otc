15/10/2025

**Wattson**
Figma
- Wireframes
	- Tenim equip?

**Hero**
**El Problema:**

> Ahir vam rebre una queixa del client que l'endpoint `/v1/manufacturing/tcu` feia timeout constant. Cada vegada que intentaven registrar un dispositiu des de Postman rebien un error `400 Bad Request` amb `"SERVER ERROR"` després de 30 segons d'espera.

**La Investigació:**

> Vaig revisar els logs de CloudWatch i vaig trobar errors repetits de `statement timeout` a la base de dades. El problema era la query `device_findByImei` que utilitzava el patró `LIKE '_${imei}'`. Aquest patró amb wildcard al principi obligava PostgreSQL a fer un full table scan (mirar tota la taula fila per fila), que era molt lent.

**La Solució:**

> l'Àlex va crear un índex funcional a la columna `don_serial_number` de la taula `dongle`. Això va optimitzar la query i ara respon immediatament en lloc de fer timeout.

**Resultat:**

> ✅ Problema resolt. He validat amb `curl` que l'API respon en menys d'1 segon.  
> ✅ El client ja pot continuar treballant normalment.  
> ✅ Les alarmes de CloudWatch s'han normalitzat.

