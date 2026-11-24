# SonarQube PMD Plugin — P3C Fork

基于上游 [jborgers/sonar-pmd 3.5.1](https://github.com/jborgers/sonar-pmd) 构建的
SonarQube PMD 插件，内置 **阿里巴巴 Java 开发规范（P3C）** 规则集。

## 兼容性

| 项目 | 版本 |
|---|---|
| 插件版本 | 3.5.1-p3c-1 |
| 基线 | 上游 sonar-pmd 3.5.1 |
| PMD | 6.55.0 |
| P3C | p3c-pmd 2.1.0（56 条规则） |
| Min. SonarQube | 9.9.4 |
| Max. SonarQube | 10.5+（SonarQube 10.7 已验证可加载 9.14 API 插件） |
| Java | JDK 11+ 编译，SonarQube 10.x（Java 17/21）运行 |

> 注意：不要升级到 sonar-pmd 4.x（PMD 7），P3C 规则是 PMD 6 实现，不兼容。

## 构建

```bash
mvn -pl sonar-pmd-plugin -am package
# 产物: sonar-pmd-plugin/target/sonar-pmd-plugin-3.5.1-p3c-1.jar
```

## 安装

将 jar 放入 SonarQube 的 `extensions/plugins/`（或 `extensions/downloads/`）目录并重启，
在质量配置中启用 PMD 仓库中带 `[p3c]` 前缀的规则。

## 与上游的差异（P3C 移植点）

1. `sonar-pmd-plugin/pom.xml` — 新增 `com.alibaba.p3c:p3c-pmd:2.1.0` 依赖（排除其传递的 PMD 组件）
2. `PmdRulesDefinition` — 在 `pmd` 仓库中额外加载 `rules-p3c.xml` + P3C 描述
3. `resources/org/sonar/plugins/pmd/rules-p3c.xml` — 56 条 P3C 规则注册
4. `resources/org/sonar/l10n/pmd.properties` — P3C 规则名称（`[p3c]` 前缀）
5. `resources/org/sonar/l10n/pmd/rules/pmd-p3c/*.html` — P3C 规则描述
