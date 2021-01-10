.. _jetbrains-idea-config:

*******
Config
*******


idea configuration of environment
=====================================

character encodings
    Editor -- File encodings -- UTF-8

Annotation valid
    Build -- Compiler -- Annotation Processors

select jdk 8 in java Compiler
    Build -- Java Compiler -- Target bytecode version -- 8

File Type filter
    Editor -- File Types -- ActionScript -- *.idea;*.iml

original configuration
=====================================

* **idea.exe.vmoptions**

-Xms128m

-Xmx512m 


* **idea64.exe.vmoptions**

-Xms128m

-Xmx750m

add configuration
=====================================


* **other configuration**

-Xms2048m

-Xmx2048m

-Xmn1024m

-Xverify:none

-XX:SurvivorRatio=6

-XX:PermSize=256m

-XX:MaxPermSize=256m

-Xss1M-XX:+UseConcMarkSweepGC

-Dsun.awt.keepWorkingSetOnMinimize=true

-Djava.awt.im.style=on-the-spot

