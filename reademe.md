### 회원가입 수정

    name 을 모두 username 으로 변경 mvc 모두!

### HomeController.php 삭제

### welcome.blade.php 삭제

### web.php 안에 두 줄 삭제

    Route::get('/', function () {
        return view('welcome');
    });

    Route::get('/home', 'HomeController@index')->name('home');

### php artisan make:controller TimelineController

### web.php

    Route::group(['middleware' => ['auth']], function(){
        Route::get('/', 'TimelineController@index');
    });
    => 메인화면을 이것으로..

### home.blade.php 내용 수정 (vue확인)

    @extends('layouts.app')

    @section('content')

    <div class="container">
        <example-component></example-component>
    </div>
    @endsection

### react로 변경

    1. php artisan preset react
    2. npm install && npm run dev

### home.blade.php 내용 수정 (react확인)

    @extends('layouts.app')

    @section('content')
    <div class="container">
        <div id="root"></div>
    </div>
    @endsection

### Example.js -> index.js로 변경

    import React, { Component } from 'react';
    import ReactDOM from 'react-dom';

    export default class Index extends Component {
        render() {
            return (
                <div className='container'>
                    <div className='row justify-content-center'>
                        <div className='col-md-8'>
                            <div className='card'>
                                <div className='card-header'>Index Component</div>

                                <div className='card-body'>I'm an Index component!</div>
                            </div>
                        </div>
                    </div>
                </div>
            );
        }
    }

    if (document.getElementById('root')) {
        ReactDOM.render(<Index />, document.getElementById('root'));
    }

### 자바스크립트 변경사항이 먹지 않는이유

    npm run watch

### index.js 을 2개로 나누기

1.  App.js 생성

        import React, { Component } from 'react';

            class App extends Component {
                render() {
                    return (
                        <div className='container'>
                            <div className='row justify-content-center'>
                                <div className='col-md-8'>
                                    <div className='card'>
                                        <div className='card-header'>App Component</div>

                                        <div className='card-body'>I'm an App component!</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    );
                }
            }

        export default App;

2.  index.js

        import React, { Component } from 'react';
        import ReactDOM from 'react-dom';
        import App from './App';

        if (document.getElementById('root')) {
        ReactDOM.render(<App />, document.getElementById('root'));
        }

### Post 모델 생성

    php artisan make:model Post -m

### post migration

        Schema::create('posts', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->unsignedBigInteger('user_id')->index();
            $table->string('body', 140);
            $table->timestamps();

            $table->foreign('user_id')->references('id')->on('users')->onDelete('cascade');
        });

### Post <=> User 모델 관계맺기

    hasMany (User)
    belongsTo (Post)
