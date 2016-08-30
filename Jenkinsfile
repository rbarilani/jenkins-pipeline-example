node {

    stage name: 'Stage1: Parallel steps'
    try {
        parallel(
            phase1: { sh "echo p1; sleep 1s; echo phase1" },
            phase2: {
                def Integer exitCode = FAIL.toBoolean() ? 1 : 0;

                try {

                    sh "echo p2; sleep 2s; exit ${exitCode}"

                } catch (Throwable error) {
                    echo "ERROR CAUGHT IN PHASE2: ${error}"
                    throw error;
                }
            }
        )
        echo "run this after both phases complete without raising errors."
    } catch (Throwable error) {
        echo "ERROR CAUGHT: ${error}"
        throw error
    } finally {
        echo "run this after both phases complete no matter if successful or not."
    }

    stage name: 'Stage2'
    echo 'Stage2 Executed!'

    stage name: 'Stage 3: Promotion'
    try {
        def env = input(
            message: 'Let\'s promote baby?',
            ok: 'Just do it!',
            parameters: [choice(choices: 'staging\nproduction', description: 'Deployment environment', name: 'env')]
        )
        echo "Execute promotion to: ${env}"
    } catch (Throwable error) {
        echo "CAUGHT: ${error}"
        throw error
    }
}
