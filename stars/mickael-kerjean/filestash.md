---
project: filestash
stars: 13545
description: :file_folder: File Management Platform / Universal Data Access Gateway (without FUSE)
url: https://github.com/mickael-kerjean/filestash
---

What is this?
=============

It started as a storage agnostic Dropbox-like file manager that works with every storage protocol: FTP, SFTP, S3, SMB, WebDAV, IPFS, and about 20 more.

It grew into a universal data access platform with virtual filesystem capabilities, APIs, and Gateways to expose your data over SFTP, S3, and MCP to give LLMs a limited view of your data:

Key Features
============

-   A plugin based architecture with a minimal core that can be extended and customized through a rich ecosystem of plugins.
-   An awesome web client to access your data, built in vanilla JS, sleek, speedy, snappy, and infinitely customizable through our dynamic patch plugins.
-   A Workflow engine to enable automation and tons of integrations capabilities
-   Integrations with almost every storage system and authentication provider, with the explicit goal of supporting 100% of storage and auth technologies on the market (including unconventional ones like using WordPress as an IdP).
-   The frontend can open virtually any file format using xdg-open plugins that add renderers and additional buttons for formats not natively supported by browsers, from astronomy to embroidery and everything in between like:
    -   photography: heif, nef, raf, tiff, raw, arw, sr2, srf, nrw, cr2, crw, x3f, pef, rw2, orf, mrw, mdc, mef, mos, dcr, kdc, 3fr, erf and srw
    -   astronomy: fits, xisf
    -   science: with latex, plantuml & pandoc compilers
    -   music: mid, midi, gp4 and gp5
    -   GIS: geojson, shp, gpx, wms and dbf
    -   data engineering: parquet, arrow, feather, avro, orc, hdf5, h5, netcdf, nc, rds, rda and rdata
    -   dev: a, so, o, dylib, dll, tar, tgz, zip, har, cap, pcap, pcapng and sqlite
    -   creative work: svg, psd, ai, sketch, cdr, woff, woff2, ttf, otf, eot, exr, tga, pgm, ppm, dds, ktx, dpx, pcx, xpm, pnm, xbm, aai, xwd, cin, pbm, pcd, sgi, wbmp and rgb
    -   biomedical: dicom, sam, bam, cif, pdb, xyz, sdf, mol, mol2 and mmtf
    -   autodesk: dwg and dxf
    -   adobe: psd, ai, xd, dng, postscript, aco, ase, swf
    -   3d: fbx, gltf, obj, stl, step, mesh, ifc, dae
    -   embroidery: dgt, dst, dsb, dsz, edr, exp, 10o, col, hus, inf, jef, ksm, pcm, pcs, pes, sew, shv, sst, tap, u01, vip, vp3 and xxx
-   Themes:  
    
-   ... and much much more (chromecast support, on demand video transcoding, mounting shared links as network drive, public site, antivirus, versioning, audit, quota, ....)  
    As a rule of thumb, if your problem involves files, we either already have a plugin for it or can make a plugin for it

Getting Started
===============

To install Filestash, head to the Getting started guide.

If you want to leverage plugins, head over to the inventory, or learn about developing your own plugins

Vision & Philosophy
===================

Our goal is simple: **to build the best file management platform ever made. Period.** But "best" means different things to different people, and making Filestash modular is the only sane model to accomplish that. Anything that isn't a fundamental truth of the universe and might spark a debate belongs in a plugin. Literally every piece listed in the key features is a plugin you can swap for another implementation or remove entirely.

This modularity is made possible by the magic of programming interfaces. For example, if you want a Dropbox-like frontend for FTP, you will find out the FTP plugin simply implements this interface:

type IBackend interface {
	Ls(path string) (\[\]os.FileInfo, error)           // list files in a folder
	Stat(path string) (os.FileInfo, error)           // file stat
	Cat(path string) (io.ReadCloser, error)          // download a file
	Mkdir(path string) error                         // create a folder
	Rm(path string) error                            // remove something
	Mv(from string, to string) error                 // rename something
	Save(path string, file io.Reader) error          // save a file
	Touch(path string) error                         // create a file

	// I have omitted 2 other methods, a first one to enable connections reuse and
	// another one to declare what should the login form be like.
}

There are interfaces you can implement for every key component of Filestash: from storage, to authentication, authorisation, custom apps, search, thumbnailing, frontend patches, middleware, endpoint creation and a few others documented in the plugin development guide.

To see what's currently installed in your instance, head over to /about. The inventory of plugins is documented here

Support
=======

-   Commercial Users → support contract
-   For individuals → #filestash on IRC (libera.chat).

Want to help us sprinkle some toppings on our noodle cups?

-   Bitcoin: `3LX5KGmSmHDj5EuXrmUvcg77EJxCxmdsgW`
-   Open Collective

Credits
=======

Filestash stands on the shoulder of: contributors, folks developing awesome libraries, a whole bunch of C stuff (the C standard library, libjpeg, libpng, libgif, libraw and many more), fontawesome, material, Browser stack to let us test on real devices, and the many guys from Nebraska and elsewhere who have been thanklessly maintaining the critical pieces that Filestash sits on top:
