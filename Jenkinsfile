pipeline
{
    agent any
    stages
    {
        stage('Continuous Download')
        {
            steps
            {
                script
                {
                    try
                    {
                     git 'https://github.com/intelliqittrainings/maven.git'   
                    }
                    catch(Exception e1)
                    {
                      mail bcc: '', body: '''Hello, 

The code did not download, please review code and advise.

Thank you,
Rufus''', cc: 'ayamnoeloa@gmail.com', from: '', replyTo: '', subject: 'Code failed to download', to: 'rufuayam@gmail.com'
exit(1)
                    }
                }
            }
        }
       stage('Continuous Build')
        {
            steps
            {
                script
                {
                    try
                    {
                       sh 'mvn package'  
                    }
                    catch(Exception e2)
                    {
                     mail bcc: '', body: '''Hello, 

The code has failed to build, please review code and advise.

Thank you,
Rufus''', cc: 'ayamnoeloa@gmail.com', from: '', replyTo: '', subject: 'Code failed to Build', to: 'rufuayam@gmail.com'
exit(2)
                    }
                }
            }
        } 
        stage('Continuous Deployment')
        {
            steps
            {
                script
                {
                    try
                    {
                      deploy adapters: [tomcat9(credentialsId: '0a2bd3e0-f7a7-42d4-81c9-a770f039ca67', path: '', url: 'http://172.31.8.33:8080')], contextPath: 'testapp', war: '**/*.war'  
                    }
                    catch(Exception e3)
                    {
                       mail bcc: '', body: '''Hello, 

The code has failed to into the QA enironment. please review code and advise.

Thank you,
Rufus''', cc: 'ayamnoeloa@gmail.com', from: '', replyTo: '', subject: 'Dployment into QA enironment fialed', to: 'rufuayam@gmail.com'
exit(3)
                    }
                }
            }
        }
         stage('Continuous Testing')
        {
            steps
            {
                script
                {
                    try
                    {
                      git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/Declarativepipeline/testing.jar'  
                    }
                    catch(Exception e4)
                    {
                     mail bcc: '', body: '''Hello, 

Continuoous TEsting on Selenium test code did not work. please review code and advise.

Thank you,
Rufus''', cc: 'ayamnoeloa@gmail.com', from: '', replyTo: '', subject: 'Selenium Test Code failure', to: 'rufuayam@gmail.com'
exit(4)
                    }
                }
            }
        }
        stage('Continuous Delivery')
        {
            steps
            {
                script
                {
                    try
                    {
                       deploy adapters: [tomcat9(credentialsId: '0a2bd3e0-f7a7-42d4-81c9-a770f039ca67', path: '', url: 'http://172.31.8.82:8080')], contextPath: 'prodapp', war: '**/*.war' 
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: '''Hello Delivery Manager

Continuoous Delivery into the production environment  did not work. please review code and advise.

Thank you,
Rufus''', cc: 'ayamnoeloa@gmail.com', from: '', replyTo: '', subject: 'Deployment into the prod server failed', to: 'rufuayam@gmail.com'
exit(5)
                    }
                }
            }
        }
    }
}
