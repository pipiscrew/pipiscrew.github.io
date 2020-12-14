---
title: PDB Downloader
author: PipisCrew
date: 2016-03-10
categories: [app]
toc: true
---

To inject that breakpoint, we typically get a manual dump of the process, and use Debug Diagnostics, or the Visual Studio Debugger, to download them.

These debuggers will attempt to download all the symbols for libraries used within the application. This is a very time consuming process because it downloads PDBs for ALL libraries, while we need the PDB file for say, one specific library in which the breakpoint is to be injected. Not to mention the PDBs for all libraries in a process can get very large in size.

http://blogs.msdn.com/b/webtopics/archive/2016/03/08/pdb-downloader.aspx

origin - http://www.pipiscrew.com/?p=4333 pdb-downloader