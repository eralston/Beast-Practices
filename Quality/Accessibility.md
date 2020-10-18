# Accessibility
---

Accessibility is the standard and practice of making content and designing its experiences to be open to everyone.  

Great accessibility is primarily a function of UX and is therefore something that must be considered at the very start of the development process [1]. As empathy and understanding is the foundation of good design, understanding that the methods and abilities to consume content are as rich and varied as human themselves. It is important to give as much control and many options as possible to empower our users to use our products successfully.  Therefore, content should be created in a way that is accessible to users who may have:

- Colorblindness, low vision, blindness, photosensitivity, or other vision difference.

- Less or different mobility.

- Deafness or hearing loss.

- Cognitive disabilities.

## Why
---

The driver for improved accessibility can be summarized into four main categories.

- **Ethical** More than ever, technology can and should be used to empower individuals who have traditionally been left behind.

- **Universal Design and Quality**\
Designing for accessibility can improve the experience for everyone (situational experiences like bright lights or no headphones).

- **Business** Between 15 -- 20% of the population has a disability, which is a lot of potential customers and a lot of spending power.   

- **Legal** Laws require equal access, particularly for government entities. Lawsuits around web accessibility are on the rise.

_"The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect."_ Sir Tim Berners-Lee

What
----

Accessibility as it pertains to web content is driven by the Web Content Accessibility Guidelines (WGAC). The current standard is WGAC 2.0, although the WGAC 2.1 was published June 2018 and has been formally adopted in Europe [3].  

The four main guiding principles for web content as defined by the WCAG 2.0(Web Content Accessibility Guidelines)

- **Perceivable** Information and user interface components must be presentable to users in ways they can perceive.

- **Operable** User interface components and navigation must be operable, meaning they must be identifiable and actionable. For example, users must be able to find the save button and activate it with a mouse, keyboard, or voice action.

- **Understandable** This means that users must be able to understand the information as well as the operation of the user interface. It must be predictable, easy to remember, and clear. The interface should help users avoid and correct mistakes.

- **Robust** Content must be robust enough that it can be interpreted reliably by a wide variety of user agents, including assistive technologies and mobile devices.

WCAG 2.0/2.1 standards have been adopted by many, if not most, government agencies worldwide. In the United States, the applicable regulation is Section 508, which mandates that the federal government must use and procure intranet and internet websites that are accessible for everyone [5].

## Principles in Detail
---
Here are key accessibility principles that guide the design and construction of our product suite. These principles are not exhaustive and should be consumed as a baseline.  They are also a replacement for true accessibility testing, user research, and user feedback.  

### Assistive Devices

While this may also be coupled under Visual accessibility for screen readers, designing for assistive devices is a critical component with many facets. The engineering of designing for assistive devices can also be complex, with strong knowledge of [ARIA and semantic HTML <https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA>](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA).

1. **Is the structure logical?** The product should be structurally and semantically relevant by providing a logical layout (for example, h1 tags preceding h2 tags). Tables should have table headers and should never be used for layout purposes.

2. **Are elements semantically relevant or make use of ARIA attributes?** Elements should use the most semantically relevant version (such as nav over div). Otherwise, ARIA attributes should be used to provide additional context, hide decorative elements, or simply augment the accessibility tree. [More info <https://developers.google.com/web/fundamentals/accessibility/semantics-aria/>](https://developers.google.com/web/fundamentals/accessibility/semantics-aria/)

3. **Does the product offer multiple ways to display full navigation?** Because users may access the application with a variety of methods, the users should be able to view navigation in multiple contexts (for example, a navigation header as well as a site map).

4. **Do links make sense out of context?** Links must be descriptive out of the context of the immediate surroundings, as they may be accessed with a keyboard (such as tabbing through links) and should provide meaningful information on where they go (e.g., no javascript void).

This is a broad simplification of a complex topic. There are screen reader tools (JAWS [<https://www.freedomscientific.com/products/software/jaws/>](https://www.freedomscientific.com/products/software/jaws/), NVDA [<https://www.nvaccess.org/>](https://www.nvaccess.org/) , VoiceOver [<https://www.apple.com/accessibility/mac/vision/>](https://www.apple.com/accessibility/mac/vision/), tota11y [<http://khan.github.io/tota11y/>](http://khan.github.io/tota11y/)) that can and should be used to check the website for compatibility, but it will not be as thorough as having non-sighted users provide feedback on a website. Websites can be built for accessibility, but not designed for accessibility, and therefore fail.  

<https://webaim.org/techniques/screenreader/>\
<https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html>

### Visual

Sites must be flexible enough to accommodate a spectrum of visual acuity and robust enough for assistive devices like screen readers. This is the broadest scope of design for accessibility.

1. **Does the product provide high contrast?** While the designers can customize the products to any set of colors, they should be encouraged to use high contrast for readability. Default generated items should pass the WGAC 2.0 contrast specification <https://webaim.org/articles/contrast/#ratio>

2. **Is meaning conveyed in multiple ways?** Colors and images must not be the only method used to convey meaning---they must be accompanied by text and/or alt-text, unless the image is purely decorative (e.g. font awesome icon). https://a11yproject.com/posts/alt-text/

3. **Can users easily skip long or confusing pieces of text?** There should be an ability to skip to content that is meaningful to the user.

4. **Is unnecessary information hidden and extra contextual information provided?** Use aria-hidden and the hidden attribute to hide unnecessary data from screen readers. Conversely, extra instructional cues and indicators should be used to provide additional details to users who use screen readers. <https://webaim.org/techniques/css/invisiblecontent/>

5. **Do user or system overrides persist?** Users may manually change the contrast or magnification on their devices to better use their systems, and our products should honor that. For example, using relative units can help with text magnification. Details are here: <https://developers.google.com/web/fundamentals/accessibility/accessible-styles>

6. **If stylesheets are disabled, is the document readable and understandable?** Is the context robust enough to ensure that the page is understandable without the style sheet?

More information for visual:
<https://webaim.org/articles/visual/blind>
<https://developers.google.com/web/fundamentals/accessibility/accessible-styles>

### Hearing
While websites are more visual than auditory, we must not forget users who are deaf, hard of hearing, or have auditory processing issues.

1. **Does audio play only after user interaction?** Audio should never autoplay on your site.

2. **Are audio controls visible and high contrast?** The user must be able to easily adjust the audio.

3. **Is all content highly structured?** This key tenant of accessibility also applies to the deaf and hard of hearing to allow for better navigation and focus.

4. **Are there alternatives for sound-based alerts?** The system must not rely on sound to provide notifications.

5. **Do videos provide text transcripts or real-time captions?** While we do not control the videos our customers can upload to their environments, our own videos should have closed captions. The product should encourage users to upload text transcriptions.

6. **Is the site optimized for mobile usage?** Many deaf and hard of hearing individuals use mobile devices and rely on the haptic feedback of mobile devices.

More information:
- <https://developer.paciellogroup.com/blog/2017/02/sounding-out-the-web-accessibility-for-deaf-and-hard-of-hearing-people-part-1/>
- <https://developer.paciellogroup.com/blog/2017/03/sounding-out-the-web-accessibility-for-deaf-and-hard-of-hearing-people-part-2/>
- <https://dequeuniversity.com/class/archive/basic-concepts1/types-of-disabilities/auditory-disabilities>

### Cognitive
The new WGAC 2.1 standard includes additional guidelines around building websites for users with cognitive differences. They main key is to ensure the site is overall consistent, predicable and comprehensible---pretend that the user is unfamiliar with web sites overall.

1. **Does the site allow the users to avoid distractions?** Is content front and center, and are animations able to be minimized or removed?

2. **Does the user have control over time-sensitive content changes?** Can the users disable elements that are time sensitive, such as slideshow autoplay or autoscroll? Does the site also show reminders of time-sensitive actions like impending session timeout? <https://webaim.org/articles/evaluatingcognitive/#principles>

### Motor

The WGAC 2.1 introduces new guidelines for creating content consumable by those with motor and dexterity disabilities. Anyone who has struggled with their mobile phone can understand why this is important!

1. **Is the website error tolerant?** If the user were to accidentally trigger, is there a confirmation or undo? If there are form fields, do they allow autofill and autocomplete?

2. **Is there a skip to relevant content?** Navigating a webpage may be difficult, and the user may be using assistive technologies, keyboards, or mobile devices.Is there a way to allow users to skip to main or relevant content? Can the user search to find and jump to relevant content?

3. **Are buttons and links large enough to be easily accessed?** The target size must be at minimum 44x44 pixels unless it is inline, controlled by the user agent or system settings, or has an equivalent target.

4. **Does the site allow for flexible usage of mobile devices?** The site must be mobile optimized for users who rely on the built-in accessibility functions of mobile devices. There should never be an assumption of device orientation.

5. **Does the site allow for keyboard navigation?** As mentioned in other principles, can the site be easily navigated using only a keyboard? Have the interactions been designed in advance and make logical sense (e.g. form fields follow a logical route).

<https://www.digitala11y.com/wcag-2-1-whats-up-with-accessibility-guidelines/>

<https://uxtricks.design/blogs/ux-design/accessibility-standards/>

Additional Reading
==================

Resources and articles for further reading:
- NV Access [https://www.nvaccess.org](https://www.nvaccess.org/)
- Ally Project [https://a11yproject.com](https://a11yproject.com/)
- Tota11y http://khan.github.io/tota11y/
- axe <https://www.deque.com/axe/>
- Inclusive Design Principles [https://inclusivedesignprinciples.org](https://inclusivedesignprinciples.org/)
- Web Accessibility in Mind [https://webaim.org](https://webaim.org/)
- Constructing a POUR Website, https://webaim.org/articles/pour/
- Considering the User Perspective https://webaim.org/articles/userperspective/
- Deque's Blog <https://www.deque.com/blog/>
- Considering accessibility when designing a usability test <https://www.deque.com/blog/considering-accessibility-when-designing-a-usability-test/>
- Five digital accessibility myths busted <https://www.deque.com/blog/5-digital-accessibility-myths-busted/>
- Smashing Magazine Accessibility Category <https://www.smashingmagazine.com/category/accessibility>
- Designing for Accessibility and Inclusion <https://www.smashingmagazine.com/2018/04/designing-accessibility-inclusion/>
- Microsoft Inclusive Design <https://www.microsoft.com/design/inclusive/>