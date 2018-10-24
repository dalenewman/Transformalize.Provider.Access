# Transformalize.Provider.Access

This is an Access database provider for Transformalize.

Build the Autofac project and put it's output into Transformalize's *plugins* folder. 
For this to work, you'll need the [64-bit OLEDB driver](https://www.microsoft.com/en-us/download/details.aspx?id=13255).

### Write Usage

```xml
<add name='Bogus' mode='init' flatten='true'>
  <connections>
    <add name='input' provider='bogus' seed='1' />
    <add name='output' provider='access' file='c:\temp\junk.mdb' />
  </connections>
  <entities>
    <add name='Contact' size='1000'>
      <fields>
        <add name='Identity' type='int' primary-key='true' />
        <add name='FirstName' />
        <add name='LastName' />
        <add name='Stars' type='byte' min='1' max='5' />
        <add name='Reviewers' type='int' min='0' max='500' />
      </fields>
    </add>
  </entities>
</add>
```

This writes 1000 rows of bogus data to an Access database.

### Read Usage

```xml
<add name='BogusRead' read-only='true' >
  <connections>
    <add name='input' provider='access' file='c:\temp\junk.mdf' />
  </connections>
  <entities>
    <add name='BogusFlat' page='1' size='10'>
      <order>
        <add field='Identity' />
      </order>
      <fields>
        <add name='Identity' type='int' />
        <add name='FirstName' />
        <add name='LastName' />
        <add name='Stars' type='byte' />
        <add name='Reviewers' type='int' />
      </fields>
    </add>
  </entities>
</add>
```

This reads 10 rows of bogus data from an Access database:

<pre>
<strong>Identity,FirstName,LastName,Stars,Reviewers</strong>
1,Justin,Konopelski,3,153
2,Eula,Schinner,2,41
3,Tanya,Shanahan,4,412
4,Emilio,Hand,4,469
5,Rachel,Abshire,3,341
6,Doyle,Beatty,4,458
7,Delbert,Durgan,2,174
8,Harold,Blanda,4,125
9,Willie,Heaney,5,342
10,Sophie,Hand,2,176</pre>