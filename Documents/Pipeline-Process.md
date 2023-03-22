## CircleCi PipLine 
# First:Basic Configuration To The Environment
-node: circleci/node@5.0.2
-eb: circleci/aws-elastic-beanstalk@2.0.1
-aws-cli: circleci/aws-cli@3.1.1
# Second:Use Root User To Install The AWS Dependencies 
      - run:
          name: Install Python PIP
          command: |
            sudo apt update
            sudo apt install -y python3-pip python-dev
      - run:
          name: Install AWS CLI
          command: |
            sudo pip3 install awsebcli
# Third:Install FrontEnd Package Dependencies
      - run:
          name: Install FrontEnd Package Dependencies
          command: |
            npm run frontend:install
# fourth:Install BackEnd Package Dependencies
      - run:
          name: Install BackEnd Package Dependencies
          command: |
            npm run api:install
# Fifth:Run Lint Command On The FrontEnd
      - run:
          name: Lint FrontEnd
          command: |
            npm run frontend:lint
# Sixth:FrontEnd Build
      - run:
          name: Build FrontEnd
          command: |
            npm run frontend:build
# Seventh:Build BackEnd
      - run:
          name: Build BackEnd
          command: |
            npm run api:build
# Eighth:Deploy Step
      - run:
          name: Deploy FullApp
          # Install,Build&Deploy the Full Web App
          command: |
            npm run api:deploy
            npm run frontend:deploy
