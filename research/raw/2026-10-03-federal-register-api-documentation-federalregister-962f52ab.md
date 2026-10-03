---
url: https://www.federalregister.gov/developers/documentation/api/v1
retrieved: 2026-10-03
command: firecrawl scrape https://www.federalregister.gov/developers/documentation/api/v1 --only-main-content --json
statusCode: 200
transport: firecrawl-cli
completeness: full
title:        Federal Register        ::        API Documentation     
---
[Skip to Content](https://www.federalregister.gov/developers/documentation/api/v1#main "Skip to Content")

Legal Status

This site displays a prototype of a “Web 2.0” version of the daily
Federal Register. It is not an official legal edition of the Federal
Register, and does not replace the official print version or the official
electronic version on GPO’s govinfo.gov.


The documents posted on this site are XML renditions of published Federal
Register documents. Each document posted on the site includes a link to the
corresponding official PDF file on govinfo.gov. This prototype edition of the
daily Federal Register on FederalRegister.gov will remain an unofficial
informational resource until the Administrative Committee of the Federal
Register (ACFR) issues a regulation granting it official legal status.
For complete information about, and access to, our official publications
and services, go to
[About the Federal Register](https://www.archives.gov/federal-register/the-federal-register/about.html "About the Federal Register")
on NARA's archives.gov.


The OFR/GPO partnership is committed to presenting accurate and reliable
regulatory information on FederalRegister.gov with the objective of
establishing the XML-based Federal Register as an ACFR-sanctioned
publication in the future. While every effort has been made to ensure that
the material on FederalRegister.gov is accurately displayed, consistent with
the official SGML-based PDF version on govinfo.gov, those relying on it for
legal research should verify their results against an official edition of
the Federal Register. Until the ACFR grants it official status, the XML
rendition of the daily Federal Register on FederalRegister.gov does not
provide legal notice to the public or judicial notice to the courts.


Legal Status

# API Documentation

# FR API Documentation

FederalRegister.gov provides multiple public API endpoints.
Each endpoint is detailed below and can be explored interactively by clicking the 'Try it out' button.
At the bottom of this page in the 'Schemas' section, valid options for various inputs such as agency names are listed in detail.


FederalRegister.gov APIs do not require API keys; all you need is an HTTP client or browser.


## FR API Documentation

[/api/v1/documentation.json](https://www.federalregister.gov/api/v1/documentation.json)

Servers

/api/v1/

#### [Federal Register Documents](https://www.federalregister.gov/developers/documentation/api/v1\#/Federal%20Register%20Documents)

GET[​/documents​/{document\_number}.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Federal%20Register%20Documents/get_documents__document_number___format_)

Fetch a single Federal Register document

GET[​/documents​/{document\_numbers}.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Federal%20Register%20Documents/get_documents__document_numbers___format_)

Fetch multiple Federal Register documents

GET[​/documents.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Federal%20Register%20Documents/get_documents__format_)

Search all Federal Register documents published since 1994.

GET[​/documents​/facets​/{facet}](https://www.federalregister.gov/developers/documentation/api/v1#/Federal%20Register%20Documents/get_documents_facets__facet_)

Fetch counts of matching Federal Register Documents grouped by a facet

GET[​/issues​/{publication\_date}.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Federal%20Register%20Documents/get_issues__publication_date___format_)

Fetch document table of contents based on the print edition.

#### [Public Inspection Documents](https://www.federalregister.gov/developers/documentation/api/v1\#/Public%20Inspection%20Documents)

GET[​/public-inspection-documents​/{document\_number}.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Public%20Inspection%20Documents/get_public_inspection_documents__document_number___format_)

Fetch a single public inspection document.

GET[​/public-inspection-documents​/{document\_numbers}.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Public%20Inspection%20Documents/get_public_inspection_documents__document_numbers___format_)

Fetch multiple public inspection documents.

GET[​/public-inspection-documents​/current.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Public%20Inspection%20Documents/get_public_inspection_documents_current__format_)

Fetch all the public inspection documents that are currently on public inspection.

GET[​/public-inspection-documents.{format}](https://www.federalregister.gov/developers/documentation/api/v1#/Public%20Inspection%20Documents/get_public_inspection_documents__format_)

Search all the public inspection documents that are currently on public inspection; use the document search to find documents that have been published.

#### [Agencies](https://www.federalregister.gov/developers/documentation/api/v1\#/Agencies)

GET[​/agencies](https://www.federalregister.gov/developers/documentation/api/v1#/Agencies/get_agencies)

Fetch all agency details

GET[​/agencies​/{slug}](https://www.federalregister.gov/developers/documentation/api/v1#/Agencies/get_agencies__slug_)

Fetch a particular agency's details

#### [Images](https://www.federalregister.gov/developers/documentation/api/v1\#/Images)

GET[​/images​/{identifier}](https://www.federalregister.gov/developers/documentation/api/v1#/Images/get_images__identifier_)

Fetch the available image variants and their metadata for a single image identifier

#### [Suggested Searches](https://www.federalregister.gov/developers/documentation/api/v1\#/Suggested%20Searches)

GET[​/suggested\_searches](https://www.federalregister.gov/developers/documentation/api/v1#/Suggested%20Searches/get_suggested_searches)

Fetch all suggested searches or limit by FederalRegister.gov section

GET[​/suggested\_searches​/{slug}](https://www.federalregister.gov/developers/documentation/api/v1#/Suggested%20Searches/get_suggested_searches__slug_)

Fetch a particular suggested search

#### Schemas

Agency

DocumentField

DocumentType

Facet

PublicInspectionDocumentField

President

PresidentialDocumentType

Format

FrDate

FrYear

Section

SuggestedSearch

Topic
