# Jak zrobić żeby to działało?

Nie było łatwo XD

## Pliki

- `pipeline_workflow_generator.py' jest z tutoriala
- pliki `.yml` są wygenerowane przez ten skrypt pythonowy i poprawione ręcznie przeze mnie, prawdopodobnie możnaby lepiej napisać skrypt pythonowy żeby od razu dobrze działało i nie trzeba nic zmieniać

## Co chcemy osiągnąć?

Ogólnie chodzi o to żeby uruchomic ten pipeline w środowisku lokalnym bez użycia condora, co się okazuje nie takie proste jak powinno to być. Na ten moment pliki `.yml` są na tyle git że `pegasus-plan` wydaje sie że działa. `pegasus-run`, którego każe uruchomić planner po zakończeniu działania nie chce już za bardzo działać, ale tym się na razie nie przejnowałem bo mój scope dotyczył tylko plannera.

## Jak uruchomić planner?

W `pegasus.properties' ostatnia linijka mówi że nie używamy dzielonego systemu plików, wszystko lokalnie, a poprzedne to przykładowe CodeGeneratory, których można użyć. JsonGenerator to ten napisany przeze mnie.

W katalogu `example-workflow wykonujemy:

```
 pegasus-plan -v   --conf pegasus.properties   --dax workflow.yml   --dir pegasus-files   --sites local   --output-sites local
```

I generuje nam to wszystkie pliki potrzebne żeby workflow zadziałało. W przypadku `JsonGenerator` generuje się też json do nowego runtime.

`pegasus-plan` po zbuildowaniu pegasusa znajduje się w `pegasus/dist/pegasus-5.2.0dev/bin

## Moje przemyślenia

Zastanawiałem sie jak ten nowy runtime powinien działać. No i jeżeli to byłby osobny, standalone runtime to dużo rzeczy, które robi pegasus się chyba traci. Najlepiej jakby chyba odpalając pegasus-run, on wykrywał że chcemy uruchomić ten nasz runtime i część zarządzania i analizowania pracy runtime dalej możnaby wykonywać pegasusem.
