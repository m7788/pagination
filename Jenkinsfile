#!groovy

// Mark the code checkout 'stage'....
stage 'Checkout'
node {
	// Get some code from a GitHub repository
	git url: 'https://github.com/m7788/pagination.git'
}

stage 'package'
node {
    mvn 'clean package'
}

stage 'test'
node {
    deploy('test')
    testAlive('')
}

input '发布到生产环境？'
    
stage 'production'
node {
    deploy('prod')
    testAlive('')
}

def mvn(args) {
    sh "${tool 'M3'}/bin/mvn ${args}"
}

def deploy(env) {
	dir('target') {
		sh "mkdir -p envs/$env"
		sh "cp pagination.jar envs/$env"
	}
}

def testAlive(url) {
	sleep 3
}
