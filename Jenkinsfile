#!/usr/bin/env groovy
@Library('Banzai@main')_

import hudson.model.Result
import io.werx.banzai.LogLevel
import io.werx.banzai.BanzaiStage
import io.werx.banzai.BanzaiStages

import static hudson.model.Result.ABORTED
import static hudson.model.Result.FAILURE
import static hudson.model.Result.NOT_BUILT
import static hudson.model.Result.SUCCESS
import static hudson.model.Result.UNSTABLE

import static io.werx.banzai.LogLevel.OFF
import static io.werx.banzai.LogLevel.FATAL
import static io.werx.banzai.LogLevel.ERROR
import static io.werx.banzai.LogLevel.WARN
import static io.werx.banzai.LogLevel.INFO
import static io.werx.banzai.LogLevel.DEBUG
import static io.werx.banzai.LogLevel.TRACE
import static io.werx.banzai.LogLevel.ALL


ansiColor('xterm') {
    timestamps {

        // LogLevel Usage:
        LogLevel logLevel = DEBUG       // It's not necessary ... use the static import
        echo "setLevel to ${DEBUG}"
        log.setLevel(logLevel)
        echo "level: ${log.level}"
        echo "value: ${log.level.value}"

        // Preferred way to set Log Level:
        log.setLevel(INFO)
        echo "level: ${log.level}"

        log TRACE, "this is trace."
        log DEBUG, "this is debug."
        log INFO, "this is info."
        log WARN, "this is warning."
        log ERROR, "this is error."
        log FATAL, "this is fatal."
        log ALL, "this is all - no use case."
        log OFF, "this is off, no use cases."

        // Jenkins currentBuild.result is a String
        currentBuild.result = 'SUCCESS'
        echo "${currentBuild.result}"

        // Banzai uses hudson.model.Result
        //result.to UNSTABLE, "because"

                // banzai tasks
                def banzaiStages = new BanzaiStages()

                banzaiStages.add("1st", {
                    log INFO, "first"
                    // result UNSTABLE
                })

                banzaiStages.add("2nd", {
                    log INFO, "second"
                    // result FAILURE
                })

                banzaiStages.add("3rd", {
                    log INFO, "third"
                    // result NOT_BUILT, "just because."
                })

                parallel banzaiStages.tasks

        /*
                // BanzaiStage
                script.banzai.addStage "Stage 1", { log INFO, "First" }
                //script.banzai.addStage "Stage 2", { aStage() }
                //script.banzai.addStage "Stage 3.", third

                script.banzai.execStages()
        */
    }
}
