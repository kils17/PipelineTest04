pipeline {
    agent any
    // 환경변수를 pipeline 내에서 선언하기
    environment {
        // Jenkins Web UI에서 설정한 값을 fileName1 라는 변수에 저장
        fileName1 = "${FILE_NAME}.txt"
        // fileName2 이라는 변수에 "AnotherFile.txt" 값을 저장
        fileName2 = "AnotherFile.txt"
        // contentOfFile2 변수에 "Here is file2" 값을 저장
        contentOfFile2 = "Here is file2"
    }
    stages {
        stage('create file') {
            steps {
                echo 'create file 1, 2'
                //파일 작성1 : 내부에서 선언한 환경변수 fileName1 = 파일명 , Jenkins Web UI에서 설정한 변수 = 파일내용
                writeFile(file: fileName1, text: "${OUTPUT_TEXT}")
                //파일 작성2 : 내부에서 선언한 환경변수 fileName2 = 파일명 , contentOfFile2 = 파일내용
                writeFile(file: fileName2, text: contentOfFile2)
            }
        }
        stage('archive artifacts') {
            steps {
                echo 'save file 1, 2'
                //Jenkins 서버에 파일 1,2를 저장
                archiveArtifacts fileName1
                archiveArtifacts fileName2
            }
        }
    }
    // ※ 이 부분의 코드는 2번째 빌드에 추가했음
    // 빌드가 끝난 후 처리 
    post {
        // 빌드가 성공시에 아래 명령어가 실행된다.
        success {
            // 워크스페이스 (clone된 프로젝트 폴더)가 삭제됨
            cleanWs()
        }
    }
}
