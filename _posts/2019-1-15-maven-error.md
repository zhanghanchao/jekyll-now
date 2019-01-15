---
layout: post
title: maven采坑
---

## Intellij IDEA maven使用allure生成测试报告，但是target目录无surefire-reports目录，需要执行mvn test生成。
1. file--settings--build/build/tools maven 可查看maven的bin目录地址
2. 配置环境变量path,添加系统变量MAVEN_HOME.
3. 在pom文件夹执行mvn test。<br/>
[ERROR] No goals have been specified for this build. You must specify a valid lifecycle phase or a goal in the format <plugin-prefix>:<goal> or <plugin-group-id>:<plugin-artifact-id>[:<plugin-version>]:<goal>. Available lifecycl
e phases are: validate, initialize, generate-sources, process-sources, generate-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources
, test-compile, process-test-classes, test, prepare-package, package, pre-integration-test, integration-test, post-integration-test, verify, install, deploy, pre-clean, clean, post-clean, pre-site, site, post-site, site-deploy.
-> [Help 1]
4. 这时找了资料，需要在pom加上
    <build>
        <defaultGoal>compile</defaultGoal>
    </build>
5. 执行mvn test成功，surefire-reports文件目录生成！



