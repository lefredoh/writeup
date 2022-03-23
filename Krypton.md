Documentacion [Krypton](http://overthewire.org/wargames/krypton/) Web de retos OverTheWire

# Nivel 5 #
[overthewire.org/wargames/krypton/krypton5.html](http://overthewire.org/wargames/krypton/krypton5.html)

## The Challenge
>Este nivel es el mismo que el anterior, sin embargo, no tenemos la longitud de la clave.

### Python ###

  ```#!/usr/bin/python
  from string import *

  mjs1='SXULWGNXIOWRZJGOFLCMRHEFZALGSPDXBLMPWIQTXJGLARIYRIBLPPCHMXMGCTZDLCLKRUYMYSJTWUTXZCMRHEFZALOTMNLBLULVMCQMGCTZDLCPTBIAVPMLNVRJNSSXWTXJGLARIQPEFUGVPPGRLGOMDKWRSIFKTZYRMQHNXDUOWQTXJGLARIQAVVTZVPLMAIVZPHCXFPAVTMLBSDOIFVTPBACSEQKOLBCRSMAMULPSPPYFCXOKHLZXUOGNLIDZVRALDOACCINRENYMLRHVXXJDXMSINBXUGIUPVRGESQSGYKQOKLMXRSIBZALBAYJMAYAVBXRSICKKPYHULWFUYHBPGVIGNXWBIQPRGVXYSSBELNZLVWIMQMGYGVSWGPWGGNARSPTXVKLPXWGDXRJHUSXQMIVTZYOGCTZRJYVBKMZHBXYVBITTPVTMOOWSAIERTASZCOITXXLYJAZQCGKPCSLZRYEMOOVCHIEKTRSREHMGNTSKVEPNNCTUNEOFIRTPPDLYAPNOGMKGCZRGNXARVMYIBLXUQPYYHGNXYOACCINQBUQAGELNRTYQIHLANTWHAYCPRJOMOKJYTVSGVLYRRSIGNKVXIMQJEGGJOMLMSGNVVERRCMRYBAGEQNPRGKLBXFLRPXRZDEJESGNXSYVBDSSZALCXYEICXXZOVTPWBLEVKZCDEAJYPCLCDXUGMARMLRWVTZLXIPLPJKKLCIREPRJYVBITPVVZPHCXFPCRGKVPSSCPBXWVXIRSSHYTUNWCGIANNUNVCOEAJLLFILECSOOLCTGCMGATSBITPPNZBVXWUPVRIHUMIBPHGUXUQPYYHNZMOKXDLZBAKLNTCCMBJTZKXRSMFSKZCSSELPUMAREBCIPKGAVCYEXNOGLNLCCJVBXHXHRHIAZBLDLZWIFYXKLMPELQGRVPAFZQNVKVZLCEMPVKPFERPMAZALVMDPKHGKKCLYOLRXTSNIBELRYNIVMKPECVXHBELNIOETUXSSYGVTZARERLVEGGNOQCYXFCXYOQYOISUKARIQHEYRHDSREFTBLEVXHMYEAJPLCXKTRFZXYOZCYXUKVVMOJLRRMAVCXFLHOKXUVEGOSARRHBSSYHQUSLXSDJINXLHPXCCVNVIPXKMFXVZLTOWQLKRYTZDLCDTVXBACSDELVYOLBCWPEERTZDTYDXFAILBRYEYEGESIHCQMPOXUDMLZVVMBUKPGECEGIWOHMFXGNXPBWKPVRSXZCEEPWVTMOOIYCXURRVBHCCSSKOLXXQSEQRTAOPWNSZKMVDLCPRTRBZRGPZAAGGKZIMAPRLKVWEAZRTXXZCSDMVVZBZRWSMNRIMZSRYXIEOVHGLGNLFZKHXKCESEKEHDIFLZRVKVFIBXSEKBTZSPEEAZMVDLCSYZGGYKGCELNTTUIGMXQHTBJKXGZRFEXABIAPMIKWARVMFKUGGFYJRSIPNBJUILDSSZALMSAVPNTXIBSMO'

  abc = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

  for i in range(8,11):
    longitud = i
    #separo el texto cifrado por la longitud
    def separar(longitud,mjs1):
      res = []
      for i in range(longitud):
        string=''
        for x in range(i,len(mjs1),longitud):
          string+=mjs1[x]
        res.append(string)      
      return res
    lista = separar(longitud,mjs1)

    #obtengo los caracteres iniciales que mas se repiten en cada string y genero una nueva cadena
    iniciales=''
    for i in range(longitud):
      frecuente = {}
      for j in ascii_uppercase:
        frecuente[j]=0
      for x in lista[i]:
        frecuente[x]+=1
      s = [(k, frecuente[k]) for k in sorted(frecuente, key=frecuente.get, reverse=True)]
      iniciales+=''.join([(k) for k in sorted(frecuente, key=frecuente.get, reverse=True)])[0]
      l = ''.join([(k) for k in sorted(frecuente, key=frecuente.get, reverse=True)])[0]

    #print('iniciales:',iniciales)

    abc =          'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    posicion=      '01234567890123456789012345'
    cipher_final='BELOSZBELOSZBELOSZBELOSZBELOSZ'
    #key='KEYLENGTH'
    key=''
    #genera la key
    for i in range(longitud):
      c=abc.index(iniciales[i])
      key+=abc[c-4]

    print('key:',key)

    resultado=''
    #genera el resultado
    for i in range(len(key)):
      c=abc.index(cipher_final[i])-abc.index(key[i])
      resultado+=abc[c]

    print('resultado:',resultado,'\nlongitud:',longitud,'\n')
