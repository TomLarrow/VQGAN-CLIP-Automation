// Jenkins pipeline for VQGAN+CLIP Automation running on AMD GPU's with ROCm

pipeline{
    agent {
        docker {
            image 'rocm/pytorch​'
            label 'amdgpu'
            args '--network=host --device=/dev/kfd --device=/dev/dri --group-add=video --ipc=host --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -v $HOME/dockerx:/dockerx'
        }
    }
    stages{
        stage('test rocm'){
            steps{
                sh "hcc --version"
                sh "/opt/rocm/bin/rocminfo"
            }
        }
    }
}
