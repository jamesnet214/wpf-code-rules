# wpfcoderules

## Property Code Styles

### Property
```
public string Email { get; set; }
```

### Get Set Property
```
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; } 
}
```

### Observable Property
```
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; OnPropertyChanged(); } 
}
```

### Setter Logic Property
```
private string _email;
public string Email 
{ 
    get { return _email; } 
    set { _email = value; Something(); OnPropertyChanged(); } 
}
```
