# Ambiguous MITRE ATT&CKS Techniques

Como vimos en el artículo de [[MITRE ATT&CK]], este proyecto describe *tácticas* y *tecnicas* que han sido detectadas y utilizadas por atacantes a lo largo de los años. Algunas técnicas, como `System Network Configuration Discovery` (**T1016**), han sido utilizadas durante camapañas pero no las vuelve necesariamente maliciosas.

A esto nos referimos con **Ambiguous Techniques**, técnicas que por si solas, observando sus características, no dan evidencia suficiente para determinar un intento de ataque o actividad maliciosa. Mismo estás no son utilizadas por personal defensivo para la mitigación de posibles amenazas dado que no proveé la suficiente información.

Ahora bien, los atacantes entienden y conocen esto y utilizan técnicas de `living-of-the-land` (**lotl**).

- **LOTL Techniques**: Son técnicas que utilizan los atacantes abusando de funcionalidades legitimas, utilidades y herramientas integradas (Como podría ser [[0. PowerShell]], `WMI` ([[WMIC]]) o `PsExec` ([[Notes/4. Cybersecurity/BlueTeam/Processes detection/PsExec|PsExec]])) para *conducir actividades maliciosas* como exfiltración de datos, escalada de privilegios y movimientos laterales sin desplegar o descargar firmas de malware tradicionales.

Identificar atacantes utilizando técnicas *lotl* requiere métodos de detección deliberados y concluyentes para minimizar los *false positive*. Es decir, que al final, los análistas/ingenieros de detección deberán inferir en el motivo de estas actividades a partir de los registros de seguridad.

Por este motivo el *Center for Threat-Informed Defense* en colaboración con empresas del rubro como Crowdstrike, Fornitet, Microsoft, etc. amplió el proyecto [Summiting the Pyramd](https://center-for-threat-informed-defense.github.io/summiting-the-pyramid/) para crear el apartado [Ambiguous Technique](https://center-for-threat-informed-defense.github.io/summiting-the-pyramid/definitions/#at-definition), contemplando la metodología para determinar el contexto y disernir entre comportamientos maliciosos y legitimos.

![[Pasted image 20251001125619.png]]

------