# react-hapi-jwt-auth

> Login using JWT components

[![NPM](https://img.shields.io/npm/v/react-jwt-auth.svg)](https://www.npmjs.com/package/react-jwt-auth) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## Install

```bash
npm install --save react-hapi-jwt-auth
```

## Usage

```jsx
import React, { Component } from 'react'
import { Route, Router } from 'react-router-dom';

import axios from 'axios';//For http requests


import {JWTAuth, JWTAuthInterceptor, JWTAuthUsers, JWTAuthProfile, JWTAuthService} from 'react-hapi-jwt-auth';


class Example extends Component {

	constructor(props){
	    super(props);

	    let http = axios;

	    this.state = {
	      user: {},
	      showLogin: true
	    }

	    const self = this;

	    //Every request that is done by axios is intercepted and the auth json web token (JWT)) is included
	    const interceptor = new JWTAuthInterceptor();
	    interceptor.setHttp(http);
	    interceptor.update();
	    
	    //The service allows to get the authenticated user information
	    const jwtauth = new JWTAuthService();
	    jwtauth.setHttp(http);
	    jwtauth.getUser()
	    .then(function(user){
	      console.log(user);
	    });
	}

	//View user profile
	profile(){
		return (<JWTAuthProfile/>);
	}

	//Admin view for all the users
	adminUsers(){
    	return (<JWTAuthUsers/>);
    }

	//Show login and create user form
	login(){
		return (<JWTAuth/>);
	}

  	render () {
    	return (
      		<Router>
				<Route path="/login" component={this.login.bind(this)}/>
				<Route path="/user" component={this.profile.bind(this)}/>
				<Route path="/admin/users" component={this.adminUsers.bind(this)}/>
			</Router>
    	)
  	}
}
```

## License

MIT © [juanprietob](https://github.com/juanprietob)
