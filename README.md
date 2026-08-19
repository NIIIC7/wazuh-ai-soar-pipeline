# 🛡️ Autonomous Cyber Defense Pipeline: Wazuh SIEM/SOAR + Gemini AI + VirusTotal

Un pipeline de ciberdefensa autónomo enfocado en la **detección, enriquecimiento con Threat Intelligence, triage contextual mediante IA y respuesta automatizada ante incidentes (SOAR)**.

---

## 📄 Documentación Completa e Informe Técnico

> 📄 **[Descargar Informe Técnico de Respuesta a Incidentes (PDF)](./Informe%20del%20Examen%20de%20Respondedor%20a%20Incidentes%20de%20Seguridad%20Ofensiva%20%281%29.pdf)**

Te invito a consultar la documentación completa de este proyecto en el archivo PDF adjunto en el repositorio. En el informe encontrarás:
* **Arquitectura de red y diagramas de flujo operativo** en entorno de laboratorio (Windows 11 & Linux Mint).
* **Logs JSON estructurados** de Wazuh, reglas de correlación personalizadas y consultas vía API.
* **Integración con Gemini AI** para la generación de diagnósticos defensivos en tiempo real.
* **Evidencias del módulo Active Response (`remove-threat.sh`)** ejecutando contención y remediación automática.
* **Análisis forense post-incidente** y validación de estado del sistema.

---

## 🚀 Visión General del Proyecto

Esta solución integra un ecosistema SOAR para reducir los tiempos de respuesta operativa en un Centro de Operaciones de Seguridad (SOC):

1. **Monitoreo & Detección:** **Wazuh SIEM** mediante monitoreo de integridad de archivos (FIM/Syscheck).
2. **Threat Intelligence:** Consultas automáticas a la **API de VirusTotal** para extraer reputación e IoCs (Hashes MD5/SHA256).
3. **Análisis Contextual con IA:** Integración con **Google Gemini AI** para auditar y generar resúmenes ejecutivos/técnicos de las alertas JSON sin intervención manual.
4. **Respuesta Automatizada (SOAR):** **Wazuh Active Response** ejecuta contención y aislamiento directo en los endpoints afectados.

---

## 🏛️ Arquitectura del Sistema

```text
[ Endpoints (Win11 / Linux Mint) ]
             │
             │ (Agente FIM / Syscheck)
             ▼
   [ Wazuh Manager Server ]
        │          │
        │          ├─────────────────────────► [ VirusTotal API ] (Threat Intel)
        │          │
        │          └─────────────────────────► [ Gemini AI API ] (Triage Contextual)
        ▼
[ Active Response ] ──► (Remediación / Script remove-threat.sh)
```

---

## 🔬 Flujo de Pruebas y Validación

La arquitectura fue validada simulando la introducción de artefactos maliciosos y de prueba (`CalcForkbomber.A.bat` y `EICAR`):
* **FIM (Regla 87105 / Nivel 12):** Captura en tiempo real de la creación del artefacto.
* **Enriquecimiento VirusTotal:** Confirmación de reputación dañina (hasta 61/66 motores).
* **Enriquecimiento Gemini (Regla 100210):** Generación automática de resumen contextual.
* **Active Response:** Ejecución de `remove-threat.sh` y eliminación inmediata del vector de amenaza.

---

## 🛠️ Tecnologías Utilizadas

* **SIEM / SOAR:** Wazuh Manager & Active Response
* **IA / LLM:** Google Gemini API
* **Threat Intelligence:** VirusTotal API
* **Sistemas Operativos:** Ubuntu Server 24.04 LTS, Windows 11, Linux Mint 22.3
* **Lenguajes & Módulos:** Bash Shell Scripting, Python, JSON Parsing, Reglas XML de Wazuh

---

📌 *Para detalles sobre reglas, bloques de configuración de `ossec.conf` y evidencias forenses, revisa el [Informe en PDF](./Informe%20del%20Examen%20de%20Respondedor%20a%20Incidentes%20de%20Seguridad%20Ofensiva%20%281%29.pdf).*
