pipeline {
	agent any

	stages {
		stage("Copy Environment Variable File") {
			steps {
				script {
				// withCredentials : Credentials 서비스를 활용하겠다

				// file : secret file을 불러오겠다
				// credentialsId : 불러올 file의 식별 ID, credentials 생성 당시 작성한 ID
				// variable : 블록(script) 내부에서 사용할 변수명
				withCredentials([file(credentialsId: 'env-file', variable: 'env_file')]) {
					// 젠킨스 서비스 내 .env 파일을
					// 파이프라인 프로젝트 내부로 복사
					sh 'cp $env_file ./.env'

					// 파일 권한 설정
					// 소유자 : 읽기 + 쓰기
					// 그 외(그룹, 다른 사용자) : 읽기 권한
					// 복습 ) 권한 : 읽기 4 : 쓰기 2 : 실행 1
					sh 'chmod 664 .env'

					}
				}
			}
		}
	}
	
	stage("Docker Image Build & Container Run") {
		steps {
			script {
				sh 'docker compose build'
				sh 'docker compose down'
				sh 'docker compse up -d'
			}
		}
	}
}
