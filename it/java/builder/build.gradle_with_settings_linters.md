```gradle
plugins {
    id 'java'
    id 'jacoco'
    id 'com.diffplug.spotless' version '8.0.0'
    id 'checkstyle'
    id 'pmd'
}

jacoco {
    toolVersion = '0.8.14'
}

group = 'org.example'
version = '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    implementation platform('org.junit:junit-bom:5.10.0')
    implementation 'org.junit.jupiter:junit-jupiter'
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}

spotless {
    java {
        palantirJavaFormat()
        forbidWildcardImports()
    }
}


checkstyle {
    toolVersion = '13.3.0'
}

pmd {
    ignoreFailures = false
    consoleOutput = true
    toolVersion = "7.19.0"
    threads = 2
    ruleSetFiles = files("config/pmd/pmd-ruleset.xml")
    ruleSets = [] // disable default rules
}

tasks.withType(Checkstyle).configureEach {
    reports {
        html.required = true
    }
}

jacocoTestReport {
    reports {
        html.required = true
    }
    afterEvaluate {
        classDirectories.setFrom(files(classDirectories.files.collect {
            fileTree(dir: it, exclude: ["/**/*Test.*"])
        }))
    }
}

jacocoTestCoverageVerification {
    violationRules {
        rule {
            limit {
                counter = 'LINE'
                minimum = 0.7
            }
            limit {
                counter = 'BRANCH'
                minimum = 0.80
            }
        }
    }
}

test {
    testClassesDirs += sourceSets.main.output.classesDirs
    classpath += sourceSets.main.runtimeClasspath

    useJUnitPlatform()
}

build {
    dependsOn spotlessCheck
}
check.finalizedBy jacocoTestReport, jacocoTestCoverageVerification
```