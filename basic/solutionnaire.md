# Atelier Python : introduction de base

---

## Solutionnaire

        #! /usr/bin/env python
        # -*- encoding: utf-8 -*-

        if __name__ == '__main__':
            import feedparser
            
            # capter le flux RSS
            url = "http://montrealpython.org/fr/feed/"
            flux = feedparser.parse(url)
            
            # retenir le nombre d'items voulus
            #items = flux['items']     # tous
            items = flux['items'][0:5]  # 5 derniers items car déjà triés par .updated
            
            # traiter les items retenus
            reply = u'Les 5 dernières modifications du site de Montréal-Python :'
            for i in items:
                # reply = chaîne unicode où placeholders %s substitués par valeurs dans tuple
                #reply = reply + u'\n%s : %s (%s)' % (i['link'], i['title'], i['updated'])
                reply = reply + u'\n%s : %s' % (i['link'], i['title'])
            
            print reply
            
En plus compact, sans les commentaires :

        #! /usr/bin/env python
        # -*- encoding: utf-8 -*-

        if __name__ == '__main__':
            import feedparser
            
            url = "http://montrealpython.org/fr/feed/"
            flux = feedparser.parse(url)

            items = flux['items'][0:5]  # 5 derniers items car déjà triés par .updated
            
            reply = u'Les 5 dernières modifications du site de Montréal-Python :'
            for i in items:
                #reply = reply + u'\n%s : %s (%s)' % (i['link'], i['title'], i['updated'])
                reply = reply + u'\n%s : %s' % (i['link'], i['title'])
            
            print reply
            
En plus pythonesque :

        #! /usr/bin/env python
        # -*- encoding: utf-8 -*-

        if __name__ == '__main__':
            import feedparser
            
            url = "http://montrealpython.org/fr/feed/"
            flux = feedparser.parse(url)
            
            print u'Les 5 dernières modifications du site de Montréal-Python :'
            for e in flux.entries[0:5]:
                print u'\n%s : %s' % (e.link, e.title)
