---
layout: post
title: Maven ��Ŀ����ʧ�ܡ��ļ�����Ŀ¼�������﷨����ȷ��
date: 2016-06-30 01:41
author: admin
comments: true
categories: [Maven]
tags: [Maven]
---

���޸Ĺ�����Ŀ�м�� edt ʱ���� Maven ���� necc-edt-api ģ��ʱ�����Ǳ��벻��������ʾ�ˡ��ļ�����Ŀ¼�������﷨����ȷ���Ĵ���

<!-- more -->

## ������ʾ

�۲����̨��������£�
 
```
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 32.730 s
[INFO] Finished at: 2016-06-26T18:59:50+08:00
[INFO] Final Memory: 42M/336M
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-jar-plugin:2.4:jar
 (default-jar) on project necc-edt-api: Error assembling JAR: Problem creating j
ar: D:\workspaceZYH\necc_20150817\edt\api\target\necc-edt-api-2016-06-26T10:59:1
8Z.jar (�ļ�����Ŀ¼�������﷨����ȷ��) (and the archive is probably corrupt b
ut I could not delete it) -> [Help 1]
[ERROR]
```

������ʾ���Ѻ�����ȷ���ļ�����Ŀ¼�������﷨����ȷ����
�ٹ۲����ɵ�jar ���ƣ���Ȼ�� 
��necc-edt-api-2016-06-26T10:59:1 8Z.jar������Ȼ��������ð�ţ� �ǲ�����Ϊ�ļ����Ƶġ�

## ���

�鿴��ģ�� pom.xml ���ļ������ɵĲ��ԣ�
 
```xml
 <build>
 ....
        <finalName>${project.artifactId}-${maven.build.timestamp}</finalName>
 ....
 </build>
```

����ʹ���� Maven ���õ����� `${maven.build.timestamp}` �� ��������ָ��Ŀ������ʼʱ�䡣��Ȼʱ����ʱ�����Ǵ����ˡ�������ð�ţ��ġ�
 
�����ʽ����Ȼ��ȥ��ʱ���еġ�����
 
������ʱ����и�ʽ����ʹ��������һ�� Maven ���õ���������ʽ��ʱ�䣬���£�

pom.xml ������£�
 
```
<properties>
...
    <maven.build.timestamp.format>yyyy-MM-dd</maven.build.timestamp.format>
...
</properties>
```

�ٴι���,�ɹ�

```
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] NECC Parent ........................................ SUCCESS [  0.885 s]
[INFO] NECC Database Table Access Component. .............. SUCCESS [  8.129 s]
[INFO] NECC Bussiness Model Component. .................... SUCCESS [  2.722 s]
[INFO] necc-edt ........................................... SUCCESS [  0.043 s]
[INFO] necc-edt-protocol .................................. SUCCESS [  1.122 s]
[INFO] NECC Core Service JAVA API Component. .............. SUCCESS [  1.605 s]
[INFO] NECC Common Component. ............................. SUCCESS [  1.600 s]
[INFO] NECC Task Runner Component. ........................ SUCCESS [  0.410 s]
[INFO] NECC Core Service JAVA IMPL Component. ............. SUCCESS [  4.209 s]
[INFO] NECC Service Facade Component. ..................... SUCCESS [  1.782 s]
[INFO] NECC Core EDT Kernel Component. .................... SUCCESS [  3.537 s]
[INFO] necc-edt-api ....................................... SUCCESS [  8.250 s]
[INFO] necc-edt-client .................................... SUCCESS [  6.947 s]
[INFO] NECC Core EDT register Component. .................. SUCCESS [  4.870 s]
[INFO] necc-edt-pump ...................................... SUCCESS [ 15.917 s]
[INFO] NECC Core EDT sync Component. ...................... SUCCESS [  3.257 s]
[INFO] NECC Task Repository Component. .................... SUCCESS [  0.456 s]
[INFO] NECC Web Government Component. ..................... SUCCESS [ 44.963 s]
[INFO] NECC Web Enterprise Component. ..................... SUCCESS [ 19.090 s]
[INFO] NECC Task Administrator Component. ................. SUCCESS [  2.860 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 02:13 min
[INFO] Finished at: 2016-06-26T19:12:38+08:00
[INFO] Final Memory: 60M/717M
[INFO] ------------------------------------------------------------------------
```
 
�����ļ���ʽΪ��necc-edt-api-2016-06-26.jar


## ���֪ʶ

Maven����6������,�������� Maven Ԥ����,�û�����ֱ��ʹ��:

* `${basedir}`��ʾ��Ŀ��Ŀ¼,������ pom.xml �ļ���Ŀ¼;
* `${version}`��ʾ��Ŀ�汾;
* `${project.basedir}`ͬ`${basedir}`;
* `${project.baseUri}`��ʾ��Ŀ�ļ���ַ;
* `${maven.build.timestamp}`��ʾ��Ŀ������ʼʱ��;
* `${maven.build.timestamp.format}`��ʾ����`${maven.build.timestamp}`��չʾ��ʽ,Ĭ��ֵΪ yyyyMMdd-HHmm,���Զ������ʽ,�����Ϳɲο�