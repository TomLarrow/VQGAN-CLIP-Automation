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
        stage('install dependencies'){
            steps{
                sh "pip install jupyterlab jupyter ipywidgets nbconvert ftfy regex tqdm omegaconf pytorch-lightning ipython einops iprogress"
                // Moving the training model download to a separate job so we don't have to waste bandwidth downloading every time
                // sh "curl -L 'https://heibox.uni-heidelberg.de/d/8088892a516d4e3baf92/files/?p=%2Fconfigs%2Fmodel.yaml&dl=1' > vqgan_imagenet_f16_1024.yaml"
                // sh "curl -L 'https://heibox.uni-heidelberg.de/d/8088892a516d4e3baf92/files/?p=%2Fckpts%2Flast.ckpt&dl=1' > vqgan_imagenet_f16_1024.ckpt"
                // sh "curl -L 'https://heibox.uni-heidelberg.de/d/a7530b09fed84f80a887/files/?p=%2Fconfigs%2Fmodel.yaml&dl=1' > vqgan_imagenet_f16_16384.yaml"
                // sh "curl -L 'https://heibox.uni-heidelberg.de/d/a7530b09fed84f80a887/files/?p=%2Fckpts%2Flast.ckpt&dl=1' > vqgan_imagenet_f16_16384.ckpt"

                copyArtifacts flatten: true, projectName: 'vc-dependencies', selector: lastSuccessful()
                // sh "git clone https://github.com/openai/CLIP"
                // sh "git clone https://github.com/CompVis/taming-transformers"
            }
        }
        stage('run'){
            steps{
                sh "jupyter nbconvert --to notebook --execute VQGAN+CLIP.ipynb"
            }
        }
    }
}