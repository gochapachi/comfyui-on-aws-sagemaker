# comfyui-on-aws-sagemaker
This repo provides easy step by step process to install confyui on aws sagemaker
# Install a separate conda installation via Miniconda
WORKING_DIR=/home/ec2-user/SageMaker

mkdir -p "$WORKING_DIR"

wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.5.2-0-Linux-x86_64.sh -O "$WORKING_DIR/miniconda.sh"

bash "$WORKING_DIR/miniconda.sh" -b -u -p "$WORKING_DIR/miniconda" 

rm -rf "$WORKING_DIR/miniconda.sh"

# Create a custom conda environment

source "$WORKING_DIR/miniconda/bin/activate"

KERNEL_NAME="comfyui"

PYTHON="3.10.6"

conda create --yes --name "$KERNEL_NAME" python="$PYTHON"

conda activate "$KERNEL_NAME"

pip install --quiet ipykernel

# Install ComfyUI in the terminal.

cd SageMaker

git clone https://github.com/comfyanonymous/ComfyUI

cd ComfyUI

pip install -r requirements.txt

pip install torch torchvision



# Run ComfyUI

1) Launch ComfyUI in Terminal 1.

source /home/ec2-user/SageMaker/miniconda/bin/activate

conda activate comfyui

python main.py --disable-xformers


2) Run Ngrok in Terminal 2.

Sign up (or log in) to the ngrok dashboard and get your Authtoken. The ngrok agent uses the authtoken to log into your account when you start a tunnel.

Open another Terminal.

Copy the value and run this commands:

- Install the ngrok agent

- Add the authtoken in your terminal

- Start a tunnel


# Install ngrok will be used later while using api

source /home/ec2-user/SageMaker/miniconda/bin/activate

conda activate comfyui

pip install pyngrok

ngrok config add-authtoken your_authtoken

cp /home/ec2-user/.config/ngrok/ngrok.yml /home/ec2-user/SageMaker/ngrok.yml

ngrok http http://localhost:8188 --basic-auth 'username:password'    or ngrok http http://localhost:8188  to continue without authentication

[Change username and password accordingly.]

# ComfyUI Start scripts after Stop and Start using Ngrok

# comfyui-start.sh Script for comfyui


source /home/ec2-user/SageMaker/miniconda/bin/activate

conda activate comfyui

python main.py


# comfyui-ngrok-start.sh script for ngrok and ssl

source /home/ec2-user/SageMaker/miniconda/bin/activate

conda activate comfyui

cp /home/ec2-user/SageMaker/ngrok.yml /home/ec2-user/.ngrok2/ngrok.yml

ngrok http http://localhost:8188/ --basic-auth 'username:password'



# ComfyUI Manager

Installation

# ComfyUI Manager - Installation

cd custom_nodes

git clone https://github.com/ltdrdata/ComfyUI-Manager.git







