# Secure erase workflow task

(no tracking assigned)

## Background

With the formal creation of [SKU packs](../in-progress/sku_packs.md), we would
like to have a place where outside organizations can create SKU packs and
register them for general availability and download. We'd like to host a
simple registry where SKU pack files can be listed and identified for easy
download and installation into RackHD.

The overall goal is to support a community of resources that are easily available
for use with RackHD in supporting a wide variety of hardware resources.

## Goals

 - Create a simple registry hosted on the internet where SKU packs can be listed

Open questions for discussion:

 - how should we accept or allow additions to this registry
 - should we have metadata associated with a SKU pack outside of the SKU pack itself
 - should we have any explicit validation process associated with a publically available SKU pack?
 - do we wish to support signing or validation of the SKU packs, to be included
 within RackHD as a part of validation when loading a SKU pack?
 - SKU packs could include vendor-specific proprietary tooling, so would be most appropriate to allow for download from their own sites, where they may wish to enable license agreements
 for using the SKU pack

## API
