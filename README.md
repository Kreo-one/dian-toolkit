# DIAN Toolkit for Electronic Invoicing and Payroll in Colombia

This repository contains the official toolkits and documentation provided by the Dirección de Impuestos y Aduanas Nacionales (DIAN) for the implementation of Electronic Invoicing (Facturación Electrónica - FE) and Electronic Payroll (Nómina Electrónica) in Colombia.

## Overview

This repository is divided into two main components:

1.  **`Caja-de-herramientas-FE-V1-9/`**: Toolkit for Electronic Invoicing, version 1.9.
2.  **`Caja-de-Herramientas-Nomina-Electronica-V1-0/`**: Toolkit for Electronic Payroll, version 1.0.

These toolkits provide all the necessary technical resources for developers to build and integrate systems that comply with the DIAN's regulations for electronic documents.

## `Caja-de-herramientas-FE-V1-9` (Electronic Invoicing Toolkit v1.9)

This directory contains the resources for implementing electronic invoicing.

### Directory Structure

*   **`Anexo Tecnico/`**: Contains the main technical annex documents in PDF format, which describe the functional and technical specifications. It also includes related documents like product and service classifiers.
*   **`Documentos de apoyo - Ingles/`**: Contains supporting documents in English, including an introduction to Schematron.
*   **`Ejemplificaciones/`**: Provides example XML files for various electronic invoicing scenarios.
*   **`Listas de valores/`**: Contains `.gc` files that represent value lists used in the XML schemas (e.g., country codes, currency types, payment methods).
*   **`Schemes/`**: Includes Schematron (`.sch`) files for validating the business rules of the XML files.
*   **`XSD/`**: Contains the XML Schema Definition (`.xsd`) files that define the structure of the electronic invoice XML documents.
*   **`XSL/`**: Contains XSLT (`.xsl`) files used for transformations, such as generating a graphical representation of the invoice.

## `Caja-de-Herramientas-Nomina-Electronica-V1-0` (Electronic Payroll Toolkit v1.0)

This directory contains the resources for implementing electronic payroll.

### Directory Structure

*   **`Anexo Tecnico/`**: Contains the main technical annex document in PDF format, which describes the functional and technical specifications for electronic payroll.
*   **`Ejemplificaciones/`**: Provides example XML files for electronic payroll scenarios, including individual payroll and adjustment notes.
*   **`Schemes/`**: Includes common UBL (Universal Business Language) schemas that the electronic payroll documents are based on.
*   **`XSD/`**: Contains the XML Schema Definition (`.xsd`) files that define the structure of the electronic payroll XML documents.

## How to Use These Resources

Developers should use these toolkits as the primary reference for implementing electronic invoicing and payroll systems in Colombia.

1.  **Start with the `Anexo Tecnico`**: Read the technical annex documents to understand the legal and technical requirements.
2.  **Use the `XSD` files**: These schemas are essential for validating the structure of the XML files your system generates.
3.  **Refer to the `Ejemplificaciones`**: The example XML files provide practical templates for different use cases.
4.  **Implement Validation**: Use the Schematron files in the `Schemes` directory to validate your generated XML against the DIAN's business rules.

This repository is a valuable resource for any developer working with Colombian electronic documents.

## Analysis of DIAN Assets

This section provides a more detailed analysis of the key technical assets in this repository.

### XSD Schemas

The XSD schemas define the structure of the XML documents for electronic invoicing and payroll. Below is an analysis of the main schemas.

#### Electronic Payroll Schemas (`Caja-de-Herramientas-Nomina-Electronica-V1-0/XSD/`)

*   **`NominaIndividualElectronicaXSDV1.0.6.xsd`**: This is the main schema for individual electronic payroll documents. It defines the structure for elements such as:
    *   `Novedad`: Indicates if there is a new feature in the payroll.
    *   `Periodo`: Defines the payroll period.
    *   `NumeroSecuenciaXML`: Defines the sequence number of the XML document.
    *   `LugarGeneracionXML`: Defines the location where the XML document was generated.
    *   `ProveedorXML`: Defines the information of the technology provider.
    *   `InformacionGeneral`: Contains general information about the document.
    *   `Empleador`: Defines the employer's information.
    *   `Trabajador`: Defines the employee's information.
    *   `Pago`: Defines the payment information.
    *   `FechasPagos`: Contains the payment dates.
    *   `Devengados`: Contains all accrued income concepts.
    *   `Deducciones`: Contains all deduction concepts.
    *   `Redondeo`: Rounding value.
    *   `DevengadosTotal`: Total accrued income.
    *   `DeduccionesTotal`: Total deductions.
    *   `ComprobanteTotal`: Total of the voucher.
*   **`NominaIndividualDeAjusteElectronicaXSDV1.0.6.xsd`**: This schema is used for adjustment notes to the electronic payroll. It is very similar to the individual payroll schema, but includes two additional key elements:
    *   `Reemplazar`: Used when replacing a previous payroll document.
    *   `Eliminar`: Used when deleting a previous payroll document.

#### Electronic Invoicing Schemas (`Caja-de-herramientas-FE-V1-9/XSD/maindoc/`)

*   **`DIAN_UBL_Structures.xsd`**: This file contains DIAN-specific extensions to the UBL standard. The main complex types defined are:
    *   `DianExtensionsType`: The root type for DIAN-specific extensions.
    *   `InvoiceControl`: Contains data related to the invoice numbering resolution.
    *   `AuthrorizedInvoices`: Information about the authorized invoice range.
    *   `SoftwareProvider`: Information about the software provider.
    *   `AdditionalMonetaryTotal`: Additional monetary totals.
    *   `FinancialInformation`: Financial information.
    *   `AuthorizationProvider`: Information of the Authorized Provider (PA) by DIAN.
    *   `QRCode`: Information about the QRCode.
*   **`UBL-Invoice-2.1.xsd`**, **`UBL-CreditNote-2.1.xsd`**, **`UBL-DebitNote-2.1.xsd`**: These are the standard UBL schemas for invoices, credit notes, and debit notes. They are well-documented within the files themselves and are not specific to DIAN, but are the base for the electronic invoicing documents.

### Schematron Rules

Schematron is a rule-based validation language used to enforce business rules that cannot be expressed with XSD. The main Schematron file is `Caja-de-herramientas-FE-V1-9/Schemes/DIAN-UBL21-model.sch`, which includes other files. The key validation patterns are:

*   **`UBL-model`**: This pattern contains the core validation rules for the DIAN UBL 2.1 model.
    *   **UBL Extensions**: Validates the structure of the UBL extensions, ensuring that the `DianExtensions` and `ds:Signature` elements are present and correctly structured.
    *   **DianExtensions Group**: Validates the content of the `DianExtensions` group, including the invoice control, software provider, and QR code information.
    *   **Provider and Authorization Provider NIT DV**: Validates the verification digit (DV) of the technology provider's and authorized provider's NIT.
    *   **Digital Signature**: Validates the structure of the digital signature, ensuring all required elements are present.
    *   **UBL Version and Profiling**: Validates that the UBL version is "2.1" and the profile ID is "DIAN 2.0".
    *   **Document Prefix and Number**: Validates the document prefix and number against the authorized range.
    *   **Issue Date and Time**: Validates the issue date and time, including format and consistency with the authorization period.
    *   **Line Count**: Validates that the line count matches the number of invoice lines.
    *   **Document References**: Validates the references in credit, debit, and contingency invoices.
    *   **Party Information**: Validates the information of the issuer, receiver, and carrier, including the NIT DV.
    *   **Allowances and Charges**: Validates the discounts and charges at the document and line level.
    *   **Taxes and Totals**: Validates the tax totals and the legal monetary totals.