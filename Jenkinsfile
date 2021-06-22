// Jenkins pipeline for VQGAN+CLIP Automation running on AMD GPU's with ROCm

pipeline{
    agent {
        docker {
            image 'rocm/pytorch'
            label 'amdgpu'
            args '-u 0 --device=/dev/kfd --device=/dev/dri --group-add=video --ipc=host --cap-add=SYS_PTRACE --security-opt seccomp=unconfined'
        }
    }
    stages{
        stage('test rocm'){
            steps{
                sh "/opt/rocm/bin/rocminfo"
            }
        }
    }
}