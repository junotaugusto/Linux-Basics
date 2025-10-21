# 1. regex (Expressões Regulares)

Expressões regulares são uma ferramenta poderosa para fazer seleções baseadas em padrões. Elas usam notações especiais semelhantes às que já encontramos, como o curinga `*`.

Vamos passar por algumas das expressões regulares mais comuns. Elas são quase universais em qualquer linguagem de programação.

Usaremos esta frase como nossa string de teste:

```
sally sells seashells 
by the seashore
```

## 1. Início de uma linha com `^`

```
^by
```

Irá corresponder à linha `"by the seashore"`.

## 2. Fim de uma linha com `$`

```
seashore$
```

Irá corresponder à linha `"by the seashore"`.

## 3. Correspondendo a qualquer caractere único com `.`

```
b.
```

Irá corresponder a `"by"`.

## 4. Notação de colchetes `[]`

Isto pode ser um pouco complicado: colchetes permitem especificar caracteres que devem estar contidos dentro deles.

```
d[iou]g
```

Irá corresponder a: `dig`, `dog`, `dug`.

O caractere `^`, quando usado dentro de colchetes, significa **qualquer coisa exceto** os caracteres especificados nos colchetes:

```
d[^i]g
```

Irá corresponder a: `dog` e `dug`, mas não `dig`.

Os colchetes também podem usar intervalos para aumentar a quantidade de caracteres que você deseja permitir:

```
d[a-c]g
```

Irá corresponder a padrões como: `dag`, `dbg` e `dcg`.

⚠️ Atenção: colchetes diferenciam maiúsculas de minúsculas:

```
d[A-C]g
```

Irá corresponder a: `dAg`, `dBg` e `dCg`, mas não a `dag`, `dbg` e `dcg`.

---

Essas são algumas expressões regulares básicas.
