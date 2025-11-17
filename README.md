# Erlin AI Documentation

Official documentation for Erlin AI, built with Mintlify.

## Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mint) to preview documentation changes locally:

```bash
npm i -g mint
```

Run the following command at the root of your documentation:

```bash
mint dev
```

View your local preview at `http://localhost:3000`.

## Publishing Changes

Changes are deployed to production automatically after pushing to the default branch via Mintlify's GitHub app integration.

## Troubleshooting

- If your dev environment isn't running: Run `mint update` to ensure you have the most recent version of the CLI.
- If a page loads as a 404: Make sure you are running in a folder with a valid `docs.json`.

## Resources
- [Mintlify documentation](https://mintlify.com/docs)
