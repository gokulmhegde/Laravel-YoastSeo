# Follow these steps for any JS library
 
1. Add this to package.json
        "devDependencies": {
            "cross-env": "^5.1",
            "lodash": "^4.17.5",
            "resolve-url-loader": "^2.3.1",
            "snarkdown": "^1.2.2",
            "babel-plugin-transform-regenerator": "^6.26.0",
            "babel-polyfill": "^6.26.0"
        },
        "dependencies": {
            "yoastseo": "^1.57.0"
        }
 
2. Add file Presenter.js and add this code
 
        import { helpers } from 'yoastseo'
        import isObject from 'lodash/isObject'
        import forEach from 'lodash/forEach'
        import filter from 'lodash/filter'
     
        export default class Presenter {
     
            getScoresAsHTML(h, data) {
                return h('div', { className: 'yoast' },
                    h('h3', { className: 'yoast__heading' }, 'SEO'),
                    h('ul', { className: 'yoast__items' },
                        this.getScoreItemsAsHTML(h, data.seo)
                    ),
                    h('h3', { className: 'yoast__heading' }, 'Content'),
                    h('ul', { className: 'yoast__items yoast__items--bottom' },
                        this.getScoreItemsAsHTML(h, data.content)
                    )
                )
            }

            getScoreItemsAsHTML(h, items) {
                return items.map(item => this.getScoreItemAsHTML(h, item))
            }

            getScoreItemAsHTML(h, item) {
                return h('li', { className: `yoast__item yoast__item--${item.rating}` }, item.text.replace(/<(?:.|\n)*?>/gm, ''))
            }

            getScores(assessor) {
                const scores = []

                forEach (this.getScoresWithRatings(assessor), (item, key) =>
                    scores.push(this.addRating(item))
                )

                return scores
            }

            addRating(item) {
                return {
                    rating: item.rating,
                    text: item.text,
                    identifier: item.getIdentifier()
                }
            }

            getScoresWithRatings(assessor) {
                const scores = assessor.getValidResults().map(r => {
                    if (!isObject(r) || !r.getIdentifier()) {
                        return ``;
                    }
                    r.rating = helpers.scoreToRating(r.score)
                    return r
                })

                return filter(scores, r => r !== ``);
            }

        }
 
3. All the following steps should be in the same file.
 
     i. Add this import
     
        import babelPolyfill from 'babel-polyfill';
        import { Paper, ContentAssessor, Researcher, SnippetPreview } from "yoastseo";
        import SEOAssessor from 'yoastseo/src/seoAssessor';
        import zipObject from 'lodash/zipObject'
        import omit from 'lodash/omit'
        import Jed from 'jed';
        import snarkdown from 'snarkdown';
        import Presenter from 'Presenter';
 
 
    ii. Declare following variable and assign it to form ( Two way binding )
     
        text: '',
        keyword: '',
        title: '',
        description: '',
        url: '',
        titleWidth: '',
        en_locale: 'en_US',
        permalink: '',
        synonyms: '',
        seo: [],
        content: []
 
    iii. Add this function
 
        getScores(seoAssessor, contentAssessor) {
            return {
                seo: new Presenter().getScoresWithRatings(seoAssessor),
                content: new Presenter().getScoresWithRatings(contentAssessor)
            }
        },
        getScoresAsHTML(scores) {
            return new Presenter().getScoresAsHTML(h, scores);
        },
        i18n() {
            return new Jed({
                domain: `js-text-analysis`,
                locale_data: {
                    "js-text-analysis": { "": {} }
                }
            })
        }
 
    iv. On any action or form submit use this code
 
        const paper = new Paper(this.text, {
                                  keyword: this.keyword,
                                  title: this.title,
                                  description: this.description,
                                  url: this.url,
                                  metaDescription: this.metaDescription,
                                  titleWidth: this.titleWidth,
                                  locale: this.en_locale,
                                  permalink: this.permalink
                              });
        const contentAssessor = new ContentAssessor(this.i18n());
        const seoAssessor = new SEOAssessor(this.i18n());
        contentAssessor.assess(paper);
        seoAssessor.assess(paper);
        const final_scores = this.getScores(seoAssessor, contentAssessor);
        this.seo = final_scores.seo;
        this.content = final_scores.content;
        console.log(this.seo);
        console.log(this.content);

Check console log for Output

# Laravel-YoastSeo

This is Complete Laravel YoastSeo package using built in Vue Component.

After months of reasearch and figured out that there is no package built for laravel.

No good documentation of YoastSeoJS in their own repo of how to use their internal components.

So this is Vue-Component which can be used in any existing Laravel Project or in Vue Project (SPAs).

Steps to use:
 1. Use Virtual host or serve your Laravel project.
 2. Install Node and then use npm install and run npm run prod.
 3. Open the Project homepage mainly Laravel Welcome Page (ie., http://larevel-yoast-vue/  OR localhost:8080/ ) which you should see a yoast form.
 
 
 
# Special thanks to:

 1. mr-cms-yoast https://git.mreach.com/mr-cms/mr-cms-yoast
 2. netlify-cms-yoast-seo https://github.com/indigotree/netlify-cms-yoast-seo 

    thier code helped me to understand and build YoastSEO for laravel using VueJS
 
# Upcoming Features
Yoast snippet preview in couple of days
