# DIAN Toolkit for Electronic Invoicing and Payroll in Colombia

## 1. Critical Architectural Note

**This repository is NOT a Frappe application.** It is a centralized digital asset library containing the official toolkits and technical documentation provided by the Colombian Tax Authority (DIAN). Do not attempt to install it as an app using `bench install-app`. Its purpose is to serve as a version-controlled source of truth for other Kreo.one applications like `kreo-dian`.

## 2. Repository Structure

This repository is organized into the official toolkits provided by the DIAN:

### `/Caja-de-herramientas-FE-V1-9/`
- **Purpose**: Contains all technical assets for Electronic Invoicing (Facturación Electrónica - FE) version 1.9.
- **Key Contents**:
    - `Anexo Tecnico/`: The main technical annex documents in PDF format.
    - `Tablas Referenciadas/`: Official DIAN catalogs in `.xlsx` format (e.g., countries, currencies, tax types). These are the source files for our generic catalog importer.
    - `XSD/`: The official XML Schema Definitions required to validate the structure of the UBL 2.1 documents.
    - `Schemes/`: The official Schematron files used for validating business rules within the XMLs.

### `/Caja-de-Herramientas-Nomina-Electronica-V1-0/`
- **Purpose**: Contains all technical assets for Electronic Payroll (Nómina Electrónica) version 1.0.
- **Key Contents**:
    - `Anexo Técnico/`: The main technical annex documents for electronic payroll.
    - `XSD/` and `Schemes/`: The corresponding validation schemas for payroll documents.