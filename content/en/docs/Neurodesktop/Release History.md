---
title: "Release History"
linkTitle: "Release History"
weight: 5
description: >-
     Previous releases of neurodesktop
---

## 20210923
- removed faulty mriqc 0.15.2 container
- neurodesk.github.io is now starting page in firefox browser

## 20210918
- added mriqc 0.16.1 and mrtrix 3.0.3

## 20210917
- included more tools for connecting to cloud storage services (rclone, owncloud, nextcloud, davfs2, globus). For more info: [Storage](/docs/neurodesktop/storage)
- styling of desktop interface, including background wallpaper and colour scheme in terminal window
- new categories in menu system (visualization) and added more categories to tools

## 20210916
- This is the first version of the newly renamed and rebuild neurodesktop (previously vnm and neuromachine)
- containers are mounted by default from CVMFS, but this can be deactivated by adding `-e CVMFS_DISABLE=true` to the docker call
