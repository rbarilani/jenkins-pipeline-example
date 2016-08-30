node {
    
    stage 'Stage1: Parallel steps'
        try {
            parallel (
                phase1: { sh "echo p1; sleep 5s; echo phase1" },
                phase2: { 
                    def exitCode = FAIL.toBoolean() ? 1 : 0;
                    
                    try {
                        sh "echo p2; sleep 8s; exit ${exitCode}" 
                    }catch(error) {
                        echo "ERROR CAUGHT IN PHASE2: ${error}"
                        throw error;
                    }
                  
                }
            )
            
            echo "run this after both phases complete without raising errors."       
            
        }catch(error) {
            echo "ERROR CAUGHT: ${error}"
            throw error; 
        }finally{
            echo "run this after both phases complete no matter if successfull or not."       
        }
    stage 'Stage2'
        echo 'Executed!'
        
}
