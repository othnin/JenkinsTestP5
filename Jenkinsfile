
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh ''' 
                    #!/bin/bash
                    echo $PWD
                    condaEnvName=`sed -n 's/name: //p' environment.yaml`
                    echo $WORKSPACE/miniconda3/envs/$condaEnvName
                    if [ ! -d $WORKSPACE/miniconda3/envs/$condaEnvName ]
                    then
                        if [ ! -d $WORKSPACE/miniconda ]
                        then
                            wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -nv -O miniconda.sh
                            bash miniconda.sh -b -p $WORKSPACE/miniconda
                        fi
                        echo ls $WORKSPACE/miniconda
                        conda config --set always_yes yes --set changeps1 no
                        conda update -q conda
                        conda create -f environment.yaml
                    fi

                '''
            }
        }
        stage('run') {
            steps {
                sh '''
                #!/bin/bash
                source $WORKSPACE/miniconda/etc/profile.d/conda.sh
                conda activate miniconda/envs/JenkinsTestP5/
                echo 'Inside run'
                python test.py
                '''
            }
        }
    }
}
