---
project: filestash
stars: 13255
description: :file_folder: What Dropbox should have been if it was based on SFTP, S3, FTP, WebDAV, Git, and more
url: https://github.com/mickael-kerjean/filestash
---

A Dropbox-like file manager that works with every storage protocol:  
FTP • FTPS • SFTP • WebDAV • Git • S3 • NFS • SMB • Artifactory • LDAP • Mysql  
Sharepoint • Azure • CalDAV • Backblaze B2 • Minio • Storj  
IPFS • Dropbox • Google Drive • ...

What / Why ?
============

Familiar with the infamous comment from Dropbox's launch on HN? It went like this:

Once we had a great user interface for FTP, we extended the idea to virtually every storage protocol and added gateways to expose Dropbox itself as an SFTP server, closing the infamous loop, while also adding all the features we always wished Dropbox had.

Key Features
============

-   Sleek, Speedy, Snappy, works great on Desktop and Mobile
-   Extensible / Customisable / Hackable via a rich ecosystem of plugins and a Workflow engine to enable automation
-   Shared Links which you can mount locally as network drives
-   Builtin Music, Video, Image viewers with optional transcoding and Chromecast support
-   API and LLM integration via MCP with support for other S3 and SFTP Gateways.
-   Themes replicating the UX of dropbox, gdrive, github, ibm, onedrive, and more
-   ... and much much much more

Documentation
=============

-   Getting started
-   Installation
-   API and MCP
-   Plugins Inventory
-   Hardening Guide

Vision & Philosophy
===================

Our goal is simple: **to build the best file management platform ever made. Period.** But "best" means different things to different people, and making Filestash modular is the only sane model to accomplish that. Anything that isn't a fundamental truth of the universe and might spark a debate belongs in a plugin.

This modularity is made possible by the magic of programming interfaces. For example, if you want a Dropbox-like frontend for FTP, you will find out the FTP plugin simply implements this interface:

type IBackend interface {
	Ls(path string) (\[\]os.FileInfo, error)           // list files in a folder
	Cat(path string) (io.ReadCloser, error)          // download a file
	Mkdir(path string) error                         // create a folder
	Rm(path string) error                            // remove something
	Mv(from string, to string) error                 // rename something
	Save(path string, file io.Reader) error          // save a file
	Touch(path string) error                         // create a file

	// I have omitted 2 other methods, a first one to enable connections reuse and
	// another one to declare what should the login form be like.
}

There are interfaces you can implement for every key component of Filestash: from storage, to authentication, authorisation, custom apps, search, thumbnailing, frontend patches, middleware, endpoint creation and a few others.

To see what's currently installed in your instance, head over to /about. The inventory of plugins is documented here.

Roadmap
=======

There are 2 major pieces of work currently underway:

1.  Making Filestash able to open virtually anything. Thanks to plugin, we're adding support for files your browser has never heard of, from astrophysics to embroidery patterns. Concretly we have added support for:
    -   photography: heif, nef, raf, tiff, raw, arw, sr2, srf, nrw, cr2, crw, x3f, pef, rw2, orf, mrw, mdc, mef, mos, dcr, kdc, 3fr, erf and srw
    -   astronomy: fits, xisf
    -   science: with latex, plantuml & pandoc compilers
    -   music: mid, midi, gp4 and gp5
    -   GIS: geojson, shp, gpx, wms and dbf
    -   data engineering: parquet, arrow, feather, avro, orc, hdf5, h5, netcdf, nc, rds, rda and rdata
    -   dev: a, so, o, dylib, dll, har, cap, pcap, pcapng and sqlite
    -   creative work: svg, psd, ai, sketch, cdr, woff, woff2, ttf, otf, eot, exr, tga, pgm, ppm, dds, ktx, dpx, pcx, xpm, pnm, xbm, aai, xwd, cin, pbm, pcd, sgi, wbmp and rgb
    -   biomedical: dicom, sam, bam, cif, pdb, xyz, sdf, mol, mol2 and mmtf
    -   autodesk: dwg and dxf
    -   adobe: psd, ai, xd, dng, postscript, aco, ase, swf
    -   3d: fbx, gltf, obj, stl, step, mesh, ifc, dae
    -   embroidery: dgt, dst, dsb, dsz, edr, exp, 10o, col, hus, inf, jef, ksm, pcm, pcs, pes, sew, shv, sst, tap, u01, vip, vp3 and xxx
    -   there is more to come as we stumbled upon new niches and spend time talking to real people.
2.  Getting to v1.0. Filestash is already rock solid, it has been in active development for over 8 years. But the bar for v1.0 will be reached when Filestash is objectively better than Dropbox, Google Drive, and Box by every single measurable metric we care about. That's the mission.

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
