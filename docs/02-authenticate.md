# Authenticate

```ts
// auth.service.ts // authenticate service
  login(credentials): Observable<Response> {
    return this.http.post(`${API_URL}/users/authenticate`, credentials);
  }

  signup(credentials): Observable<Response> {
    return this.http.post(`${API_URL}/users`, credentials);
  }

  finishAuthentication(token): void {
    localStorage.setItem('token', token)
    this.router.navigate(['profile']);
  }

  logout(): void {
    localStorage.removeItem('token');
  }
```

```ts
// login component in angular2
  onLoginSubmit(credentials) {
    this.auth.login(credentials)
      .map(res => res.json())
      .subscribe(
        response => this.auth.finishAuthentication(response.token),
        error => this.errorMessage = error.json().message
      );
  }

  onSignupSubmit(credentials) {
    this.auth.signup(credentials)
      .map(res => res.json())
      .subscribe(
        response => this.auth.finishAuthentication(response.token),
        error => this.errorMessage = error.json().message
      );
  }
```