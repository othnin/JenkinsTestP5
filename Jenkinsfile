
pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh ''' 
                    #!/bin/bash
                    echo $PWD
                    wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -nv -O miniconda.sh
                    bash miniconda.sh -b -p $WORKSPACE/miniconda
                    conda config --set always_yes yes --set changeps1 no
                    conda update -q conda
                    conda env create -f environment.yaml

                '''
            }
        }
        stage('run') {
            steps {
                sh '''
                #!/bin/bash
                source $WORKSPACE/miniconda/etc/profile.d/conda.sh
                conda activate miniconda/envs/test/
                echo 'Inside run'
                python test.py
                '''
            }
        }
    }
}
