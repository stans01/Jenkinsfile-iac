node
{
def mavenHome = tool name: "maven3.6.3"
stage('1. Clone the code')    
{    
git branch: 'development', credentialsId: 'git', url: 'https://github.com/stans01/maven-web-app.git'
}

stage('2. Build package')
{

sh "${mavenHome}/bin/mvn clean package"

}

stage('3. Code Quality Report')
{

sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('4. UploadingArticats')
{

sh "${mavenHome}/bin/mvn clean deploy"
}

stage('5. Deploy to Tomcat')
{
    
deploy adapters: [tomcat9(credentialsId: 'tomcat_credentials1', path: '', url: 'http://54.175.18.129:7777/')], contextPath: null, war: '**/myapps.war'

}

stage('6. Email Notification')
{
emailext body: '''Hi

Build status
Stanley University
+6472900105''', subject: 'Build status', to: 'stansagbor2@gmail.com'

}
}
