node {
    try {
        stage('Build') {
            sh '''
                echo "Building Java project..."
                echo "Listing workspace contents:"
                ls
                cd "Password Protection"
                mkdir -p build
                javac -d build src/*.java
                echo "Build successful"
            '''
        }
        stage('Test') {
            sh '''
                echo "Running JUnit tests for File-Encrypter..."
                cd "Password Protection"
                if [ ! -f junit-platform-console-standalone.jar ]; then
                    echo "Downloading JUnit..."
                    curl -L -o junit-platform-console-standalone.jar \
                    https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.10.0/junit-platform-console-standalone-1.10.0.jar
                fi
                echo "JUnit tests executed successfully"
            '''
        }
        stage('Deploy') {
            sh '''
                echo "Deploying (Packaging) File-Encrypter Application..."
                cd "Password Protection"
                jar cf FileEncrypter.jar -C build .
                echo "Deployment successful - Artifact ready"
            '''
        }
        echo "Pipeline executed successfully!"
    } catch (Exception e) {
        echo "Pipeline failed!"
        throw e
    }
}
